<script setup>
import {ref, useTemplateRef, onMounted} from "vue";

const mapLeft = ref(0);
const mapTop = ref(0);
const mapRef = useTemplateRef('mapRef')
const mapSlide = function (event) {
  if (!['ArrowLeft', 'ArrowRight', 'ArrowDown', 'ArrowUp'].includes(event.code)) {
    return;
  }
  if (event.code === 'ArrowRight') {
    mapLeft.value -= 2;
  }
  if (event.code === 'ArrowLeft') mapLeft.value += 2;
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
    
    <div class="sprite-holder">
      <div class="sprite1"></div>
      
    </div>



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
</style>
