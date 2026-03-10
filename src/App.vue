<script setup>
import {ref, useTemplateRef, onMounted} from "vue";

const mapLeft = ref(0);
const mapTop = ref(0);
const mapRef = useTemplateRef('mapRef')
const spriteImage = {
  right: [
      '/right-walk0.png',
      '/right-walk1.png',
      '/right-walk2.png',
      '/right-walk3.png',
      '/right-walk4.png',
      '/right-walk5.png',
      '/right-walk6.png',
      '/right-walk7.png',
      '/right-walk8.png',
  ]
}

const sprite = ref({
  image: spriteImage.right[0],
  imageIndex: 0
})

const spriteMove = function (direction) {
  sprite.value.imageIndex = sprite.value.imageIndex === spriteImage[direction].length - 1 ? 0 : sprite.value.imageIndex + 1;
  sprite.value.image = spriteImage[direction][sprite.value.imageIndex];
}

const mapSlide = function (event) {
  if (!['ArrowLeft', 'ArrowRight', 'ArrowDown', 'ArrowUp'].includes(event.code)) {
    return;
  }
  if (event.code === 'ArrowRight') {
    mapLeft.value -= 2;
  }
  if (event.code === 'ArrowLeft') {
    mapLeft.value += 2;
  }
  spriteMove('right');
}

onMounted(() => {
  // the event listener for this element will only work when the element is focused
  mapRef.value.focus();
})


</script>

<template>
  
  <div class="map-div">
    <img class="map"
      src="/Sample.png"
      alt="the whole world"
      ref="mapRef"
      width="1800"
      height="1200"
      tabindex="0"
      @keydown="mapSlide"
      :style="{'left': + mapLeft + 'px'}"
    />
  </div>
  <div class="sprite">
    <img
        :src="sprite.image"
        alt="character"
    />
  </div>
</template>

<style scoped>
.map-div {
  position: relative;
  height: 1svh;
}

.map {
  position: absolute;
}

.sprite {
  position: absolute;
  top: 50svh;
  left: 50svw;
  z-index: 3;
}

</style>
