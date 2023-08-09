---
layout: article
title: "TWICE Dataset: Digital Twin of Test Scenarios in a Controlled Environment"
article_header:
  type: overlay
  theme: dark
  background_color: '#203028'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: /images/teste.png


---

We have developed a comprehensive dataset that includes camera, radar,
LiDAR, inertial measurement unit (IMU), and GPS sensor data recorded under adverse weather conditions in a
controlled environment. This dataset also includes the digital twin of each test scenario made in a Hardware-in-
the-Loop setup. We recorded test scenarios, some of which are catalogued by EURONCAP (European New Car
Assessment Programme), using objects of interest such as car, cyclist, truck and pedestrian. All scenarios were
recorded in the outdoor facilities of the CARISSMA Institute of Automated Driving in Ingolstadt, Germany.
The dataset contains more than 2 hours of recording, which totals more than 280GB of data. Overall, this
dataset provides a valuable resource for researchers in the field of autonomous vehicles to test and improve their
algorithms in adverse weather conditions, as well as explore the simulation-to-reality gap.

![TeXt Theme](/images/ego_front.png)
<div class="swiper my-3 swiper-demo swiper-demo--image swiper-demo--3">
  <div class="swiper__wrapper">
    <div class="swiper__slide"><img class="lightbox-ignore" src="/images/ego_front.png"/></div>
    <div class="swiper__slide"><img class="lightbox-ignore" src="https://kitian616.github.io/jekyll-TeXt-theme/docs/assets/images/cover2.jpg"/></div>
    <div class="swiper__slide"><img class="lightbox-ignore" src="https://kitian616.github.io/jekyll-TeXt-theme/docs/assets/images/cover3.jpg"/></div>
    <div class="swiper__slide"><img class="lightbox-ignore" src="https://kitian616.github.io/jekyll-TeXt-theme/docs/assets/images/cover2.jpg"/></div>
    <div class="swiper__slide"><img class="lightbox-ignore" src="https://kitian616.github.io/jekyll-TeXt-theme/docs/assets/images/cover3.jpg"/></div>
    <div class="swiper__slide"><img class="lightbox-ignore" src="https://kitian616.github.io/jekyll-TeXt-theme/docs/assets/images/cover2.jpg"/></div>
    <div class="swiper__slide"><img class="lightbox-ignore" src="https://kitian616.github.io/jekyll-TeXt-theme/docs/assets/images/cover3.jpg"/></div>
  </div>
  <div class="swiper__button swiper__button--prev fas fa-chevron-left"></div>
  <div class="swiper__button swiper__button--next fas fa-chevron-right"></div>
</div>

<script>
  {%- include scripts/lib/swiper.js -%}
  var SOURCES = window.TEXT_VARIABLES.sources;
  window.Lazyload.js(SOURCES.jquery, function() {
    $('.swiper-demo--0').swiper();
    $('.swiper-demo--1').swiper();
    $('.swiper-demo--2').swiper();
    $('.swiper-demo--3').swiper();
    $('.swiper-demo--4').swiper({ animation: false });
  });
</script>




