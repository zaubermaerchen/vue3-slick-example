<script setup lang="ts">
import { ref } from 'vue';
import Slick from '@zaubermaerchen/vue3-slick';
import 'slick-carousel/slick/slick.css';

const slickRef = ref<InstanceType<typeof Slick> | null>(null);

const slickOptions: JQuerySlickOptions = {
    autoplay: false,
    arrows: false,
    infinite: false,
    lazyLoad: 'progressive',
};

const next = () => {
    slickRef.value?.next();
};
const prev = () => {
    slickRef.value?.prev();
};

const onAfterChange = (event: JQuery.Event, slick: JQuerySlick, currentSlide: number) => {
    console.log(`after change event called. slide:${currentSlide}`);
};
const onBeforeChange = (event: JQuery.Event, slick: JQuerySlick, currentSlide: number, nextSlide: number) => {
    console.log(`before change event called. current:${currentSlide}, next:${nextSlide}`);
};
const onLazyLoaded = (event: JQuery.Event, slick: JQuerySlick, image: object, imageSource: string) => {
    console.log(`lazy loaded event called. path:${imageSource}`);
};

</script>

<template>
<Slick
  ref="slickRef"
  :options="slickOptions"
  @afterChange="onAfterChange"
  @beforeChange="onBeforeChange"
  @lazyLoaded="onLazyLoaded">
  <img data-lazy="/images/image01.png">
  <img data-lazy="/images/image02.png">
  <img data-lazy="/images/image03.png">
  <img data-lazy="/images/image04.png">
  <img data-lazy="/images/image05.png">
</Slick>
<button type="button" @click="prev">prev</button>
<button type="button" @click="next">next</button>
</template>
