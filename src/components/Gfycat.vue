<template>
  <figure class="vue-gfycat">
    <img class="gfyitem" ref="item" />
    <figcaption v-if="caption !== ''" v-html="caption"></figcaption>
  </figure>
</template>

<script>
import { gfyObject } from 'gfycat-js-embed'

export default {
  name: 'gfycat',
  props: {
    gfyId: {
      type: String,
      required: true
    },
    controls: {
      type: Boolean,
      required: false,
      default: false
    },
    title: {
      type: Boolean,
      required: false,
      default: false
    },
    autoplay: {
      type: Boolean,
      required: false,
      default: true
    },
    responsive: {
      type: Boolean,
      required: false,
      default: false
    },
    maxHeight: {
      required: false,
      default: false
    },
    gif: {
      type: Boolean,
      required: false,
      default: false
    },
    hd: {
      type: Boolean,
      required: false,
      default: true
    },
    playbackSpeed: {
      validator: function (value) {
        return value >= 0.125 && value <= 8
      },
      required: false,
      default: 1
    },
    caption: {
      type: String,
      required: false,
      default: ''
    }
  },
  mounted: function () {
    let el = this.$refs.item
    this.$item = gfyObject(el, 'gfyitem')
    this.$item.init({
      id: this.gfyId,
      controls: this.controls,
      title: this.title,
      autoplay: this.autoplay,
      responsive: this.responsive,
      maxHeight: this.maxHeight,
      optimize: false, // does not start playing with this enabled
      gif: this.gif,
      hd: this.hd,
      playbackSpeed: this.playbackSpeed
    }).catch(error => {
      // ruh-roh
    })
  }
}
</script>

<style>
.vue-gfycat {
  pointer-events: none;
}
</style>
