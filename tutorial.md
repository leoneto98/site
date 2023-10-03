---
layout: page
titles:
  # @start locale config
  en      : &EN       Tutorial
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN

  # @end locale config
key: tutorial
aside:
  toc: true
---

## Requirements:
Follow instructions of OSI Installation [available at here](https://www.asam.net/static_downloads/ASAM_OSI_reference-documentation_v3.5.0/index.html)
```python
pip install --upgrade google-api-python-client
```
### Important:
You need to change the path on the TWICE_path.txt in order to this script works (path where the folder TWICE is stored)
```python
with open('TWICE_path.txt', 'r') as f:
    path_twice = f.read()
import google.protobuf.message
import google.protobuf.json_format
import numpy as np
import cv2
import os
import matplotlib
import matplotlib.pyplot as plt
import sys
import struct
import math as m
from cuboid_project import Camera_project
import lidar_osi2PLY 
import radar_osi_plot
import file_selector
sys.path.insert(1,os.path.join(path_twice,"TWICE","open-simulation-interface"))
from osi3.osi_sensordata_pb2 import SensorData
from osi3.osi_datarecording_pb2 import SensorDataSeries
```
## File Selector
Using the code below you can select the desire scenario, with the different parameters. If you select a combination of parameters that was not recorded it will return an error. Any warnings about the scenario will be displayed.
```python
weather = "snow" # daytime, rain, night, snow
scenario = "car" #CCRb, CCRs, car, bike, pedestrian, truck, truck_perpendicular, os.path.join("CBLA","with_car"), os.path.join("CBLA","withot_car")
scenario_type = "real" # real, synthetic
radar_mode = "cluster" # cluster, object_list
test_run = 1 # Usually has 3 test_runs, but it varies from 1 to 4.

camera_path,radar_path,ego_path,obj_path,lidar_path = file_selector.file_selector(scenario,weather,scenario_type,radar_mode,test_run)
```
## Camera
The code below open the image file: You can save all the test_run in a video, or just see a frame. You also have the option to project the ground truth cuboid.

```python
pathSaveImage="/path/save_image" #path to save image and video
frame=48
showImage=False
saveVideo=False
saveImage=True
projectCuboid=True
showFrame=True
showTimestamp=True
Camera_project.project_cuboid_image(camera_path,frame,projectCuboid,showImage,saveVideo,saveImage,showFrame,showTimestamp,pathSaveImage)
```
### Output
<video width="640" height="360" controls>
  <source src="{{ site.baseurl }}/images/car_cuboid.m4v" type="video/mp4">
  Your browser does not support this video format.
</video>

## Radar
With the code below you can generate a video file from the Radar data:
```python
path_radar_video = "/path/to/save/video" #path of folder where you want to save the radar video file
save_video = True
save_frame = True
frame_n = 8
count_points = True #Cluster mode: count the number of cluster points inside object ground truth
covariance =  True # Plot covariance ellipses for cluster points
IoU = True # Object List mode: calculate the Intersection over Union of the detect rectangle with object ground truth
segmentation_data =  False #data from pc segmentation of the object
text = True #text indicating ego and object next to their respective rectangles
if radar_mode == "object_list":
    radar_osi_plot.radar_objlist_plot(radar_path,path_radar_video,save_video,save_frame,frame_n,IoU,segmentation_data,text)
if radar_mode == "cluster":
    radar_osi_plot.radar_cluster_plot(radar_path,path_radar_video,save_video,save_frame,frame_n,count_points,covariance,segmentation_data,text)
```
There are several parameters that you can choose to have appear in the video or export to a .csv file. In cluster mode, it is possible to count how many cluster points are inside the detected object, and you can also choose whether to plot the cluster covariance. In object list mode, you can calculate the Intersection over Union of the object with the radar detection. By setting the segmetation_data variable to True, a .csv file will be generated with the data of the variables just described.

### Output
#### Cluster
<video width="640" height="360" controls>
  <source src="{{ site.baseurl }}/images/radar_cluster.m4v" type="video/mp4">
  Your browser does not support this video format.
</video>

#### Object List

<video width="640" height="360" controls>
  <source src="{{ site.baseurl }}/images/radar_object_list.m4v" type="video/mp4">
  Your browser does not support this video format.
</video>

## LiDAR

Opening the LiDAR data. The LiDAR data is serialized using the struct package, just like the camera data. The code below read only the first detection of the LiDAR, to read all the data just erase the break

```python
lidar_obj = SensorData()
with open(lidar_path,'rb') as f:
    while 1:
        message_size_bytes = f.read(struct.calcsize("<L"))
        if len(message_size_bytes) == 0:
            break
        message_size = struct.unpack("<L",message_size_bytes)[0]
        message_bytes = f.read(message_size)
        lidar_obj.ParseFromString(message_bytes)
        print(lidar_obj.feature_data.lidar_sensor[0])
        break
```

Example of how to get a parameter from the lidar_obj:
```python
print(lidar_obj.feature_data.lidar_sensor[0].detection[0].intensity)
```
If you wanna convert the LiDAR data from .osi to .ply, just run the code below. It will generate one .ply file for each timestamp.
```python
path_ply_files = "/path/save/ply_files" #path of folder where you want to save the .ply files
lidar_osi2PLY.osi2ply(lidar_path,path_ply_files)
```

## General OSI data
Open .osi SensorDataSeries(ADMA, GPS and radar data) [Documentation](https://www.asam.net/static_downloads/ASAM_OSI_reference-documentation_v3.5.0/structosi3_1_1SensorDataSeries.html)
```python
obj_ego = SensorDataSeries()
path_osi_file = ego_path
with open(path_osi_file,'rb') as f:
    obj_ego.ParseFromString(f.read())
```
If you print an object of SensorDataSeries you can visualize how the data is organized inside OSI class structure. It is also useful see the diagrams that are avaible in the [OSI documentation](https://www.asam.net/static_downloads/ASAM_OSI_reference-documentation_v3.5.0/structosi3_1_1RadarDetectionData.html)
```python
print(obj_ego.sensor_data[0].sensor_view[0].global_ground_truth.stationary_object[0].base.position.x)
```
Example of how to acess the .osi data from the ego
```python
ego_position_x=[]
ego_position_y=[]
ego_time=[]
for ind in range(len(obj_ego.sensor_data)):
    ego_position_x.append(obj_ego.sensor_data[ind].sensor_view[0].host_vehicle_data.vehicle_motion.position.x)
    ego_position_y.append(obj_ego.sensor_data[ind].sensor_view[0].host_vehicle_data.vehicle_motion.position.y)
    ego_time.append((obj_ego.sensor_data[ind].sensor_view[0].timestamp.seconds)+(obj_ego.sensor_data[ind].sensor_view[0].timestamp.nanos/1000000000))
```
To acess radar data, the sensor data index changes for each timestamp. Each cluster for that timestamp is inside detection list. In the example below, the cluster_rcs variable receives the rcs value for the first timestamp detection and the first cluster within that timestamp [RadarDetectionData Documentation](https://www.asam.net/static_downloads/ASAM_OSI_reference-documentation_v3.5.0/structosi3_1_1RadarDetectionData.html)
```python
obj_radar = SensorDataSeries()
with open(radar_path,'rb') as f:
    obj_radar.ParseFromString(f.read())
```
```python
for frame in range(len(obj_radar.sensor_data)):
    for ind in range(len(obj_radar.sensor_data[frame].feature_data.radar_sensor[0].detection)): 
        rcs = obj_radar.sensor_data[frame].feature_data.radar_sensor[0].detection[ind].rcs
        print(rcs)
```

```python
```
```python
```