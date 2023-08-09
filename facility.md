---
layout: page
titles:
  # @start locale config
  en      : &EN       Facilities
  en-GB   : *EN
  en-US   : *EN
  en-CA   : *EN
  en-AU   : *EN

  # @end locale config
key: facility
aside:
  toc: true
---
## CARISSMA Outdoor
CARISSMA's outdoor test facility, located in the northeast of Ingolstadt (Germany), is used for tests with vehicles and dummies of road users. Such tests are required for the development of methods, algorithms and components as well as for their validation. The use of the systems under real conditions is intended to ensure that they are suitable for applications in vehicle safety. More can be found at: [CARISSMAOutdoor](https://www.thi.de/en/research/carissma/laboratories/outdoor-test-facility/)

<style>
  .swiper-demo {
    height: 420px;
    width: 600px;
  }
  .swiper-demo .swiper__slide {
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 3rem;
    color: #fff;
  }

</style>

<div class="swiper my-3 swiper-demo swiper-demo--image swiper-demo--3">
  <div class="swiper__wrapper">
    <div class="swiper__slide"><img class="lightbox-ignore" src="/images/outdoor_carissma.svg"/></div>
    <div class="swiper__slide"><img class="lightbox-ignore" src="/images/outdoor_aerial.jpg"/></div>


  <div class="swiper__button swiper__button--prev fas fa-chevron-left"></div>
  <div class="swiper__button swiper__button--next fas fa-chevron-right"></div>
</div>
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

## CARISSMA Hardware-in-the-loop Laboratory

 In the HIL laboratory at the CARISSMA research centre, new methods are being developed for testing complex safety systems based on environment sensors. The focus is on increasing the depth of testing and the coverage of the test space to allow efficient and consistent testing of automatic drive functions and integral safety concepts. This involves developing and analysing new test methods, for example, in the field of model-based testing, mixed reality and simulation-based sensor stimulation. In the latter case, simulated data is supplied through target simulators for actual environment and environmental sensors, as appropriate to the respective sensor. More can found at: [CARISSMA_HiL](https://www.thi.de/en/research/carissma/laboratories/hil-laboratory/)