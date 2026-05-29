<script setup lang="ts">
import { reactive, ref } from 'vue';
const containerWidth = ref<number>(800);
const containerHeight = ref<number>(600);
const src = ref<string>('./Wallpaper_Blue_Sky.png');
let cropBox = reactive<CropBox>({x:0, y: 0, width: 0, height: 0});
const containerRef = ref<HTMLDivElement>();
interface CropBox {
  x: number
  y: number
  width: number
  height: number
}

const startCrop =(e:MouseEvent)=> {
const rect = containerRef.value!.getBoundingClientRect()

const x = e.clientX - rect.left ;
const y = e.clientY - rect.top;

cropBox = {
  x:x,
  y:y,
  width:0,
  height:0
}

}

const moveCrop=()=> {
  console.log('wedwqe');
}


</script>

<template>
 <div class="container"  
 :style="{
  height: `${containerHeight}px`,
  width: `${containerWidth}px`
 }"
 ref="containerRef"
 @mousedown="startCrop"
 @mouseup="moveCrop"
 >

  <img :src="src" class="image" alt="image" />
  <div class="crop-container" 
    :style="{
    height: `${cropBox.height}px`,
    width: `${cropBox.width}px`
  }"
  ></div>

 </div>
</template>

<style scoped>
.container {
  position: relative;
  display: flex;
  justify-self: center;
  align-items: center;
  border: 1px solid black;
  overflow: hidden;
}

.image {
  position: absolute;
  top:0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: contain;
  pointer-events: none;
}
</style>
