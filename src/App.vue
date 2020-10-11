<template>
  <div id="app">
    <Carousel>
      <Slides>
          <Slide v-for="(image, index) in slides"
            :key="index"
            :id="'image-' + index"
            :isCurrent="index===currentIndex"
            :image="image.img"
            :title="image.title"
            :content="image.content"
            :takeFocus="takeFocus"
          />
      </Slides>

      <SlideNav>
        <SlideNavItem v-for="(slide, index) in slides"
          :aria-label="'Slide ' + index"
          :key="index"
          :index="index"
          :isCurrent="index === currentIndex"
          :goTo="goTo"
        />
      </SlideNav>

      <Controls>
        <IconButton v-if="isPlaying" aria-label="Pause" :click="setPlaying">
          <v-icon dark>fa-pause</v-icon>
        </IconButton>

        <IconButton v-else aria-label="Play" :click="setPlaying">
          <v-icon dark>fa-play</v-icon>
        </IconButton>

        <IconButton aria-label="Previous Slide" :click="prevSlide">
          <v-icon dark>fa-backward</v-icon>
        </IconButton>

        <IconButton aria-label="Next Slide" :click="nextSlide">
          <v-icon dark>fa-forward</v-icon>
        </IconButton>
      </Controls>
    </Carousel>
  </div>
</template>

<script>
import slides from './assets/slide.js';

import Carousel from './components/Carousel';
import Slides from './components/Slides';
import Slide from './components/Slide';
import SlideNav from './components/SlideNav';
import SlideNavItem from './components/SlideNavItem';
import Controls from './components/Control';
import IconButton from './components/IconButton';

const SLIDE_DURATION = 3000; 

export default {
  name: 'App',
  components: {
    Carousel,
    Slides,
    Slide,
    SlideNav,
    SlideNavItem,
    Controls,
    IconButton
  },
  data() {
    return {
      slides,
      currentIndex: 0,
      isPlaying: false,
      takeFocus: false,
      removeTimeOut: () => {},
    }
  },
  methods: {
    setPlaying() {
      this.isPlaying = !this.isPlaying
      this.takeFocus = false;
    },
    prevSlide() {
      this.currentIndex = (this.currentIndex - 1 + slides.length) % slides.length
      this.takeFocus = false;
    },
    nextSlide() {
      this.currentIndex = (this.currentIndex + 1) % slides.length
      this.takeFocus = false;
    },
    setup() {
      if(this.isPlaying){
        this.takeFocus = false;
        let timeout = setTimeout(() => {
        this.currentIndex = (this.currentIndex + 1) % slides.length
        }, SLIDE_DURATION)

        this.removeTimeOut = () => {
          clearTimeout(timeout)
        }
      }
    },
    goTo(index) {
      this.currentIndex = index;
      this.takeFocus = true;
    },
  },
  mounted() {
    this.setup()
  },
  updated() {
    this.removeTimeOut()
    this.setup()
  }
}

  

</script>

<style>
@import url("./assets/index.css");
</style>
