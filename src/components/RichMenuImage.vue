<script setup lang="ts">
import html2canvas from 'html2canvas'
import { ref } from 'vue'
const richmenu1 = ref<HTMLElement>()
const scale = ref(5)
const getImage = (element?: HTMLElement, filename= 'richmenu-'+new Date().toISOString()) => {
  if (!element) {
    alert('找不到該element')
    return
  }
  html2canvas(element, {
    scale: scale.value
  }).then(function (canvas) {
    const a = document.createElement('a')
    // toDataURL defaults to png, so we need to request a jpeg, then convert for file download.
    a.href = canvas.toDataURL('image/jpeg').replace('image/jpeg', 'image/octet-stream')
    a.download = filename+".jpg"
    a.click()
  })
}
</script>
<template>
  <div class="container">
    <ul class="richmenu mt-3" ref="richmenu1">
      <li class="icon icon--green">
        <i class="fa-solid fa-magnifying-glass"></i><span class="icon__text">查詢本日</span>
      </li>
      <li class="icon icon--green">
        <i class="fa-solid fa-magnifying-glass"></i><span class="icon__text">查詢本周</span>
      </li>
      <li class="icon icon--green">
        <i class="fa-solid fa-magnifying-glass"></i><span class="icon__text">查詢本月</span>
      </li>
      <li class="icon icon--white">
        <i class="fa-solid fa-angles-right"></i><span class="icon__text">下一頁</span>
      </li>
    </ul>
    <button class="mt-3" @click="getImage(richmenu1)">取得圖片</button>
  </div>
</template>
<style lang="scss" scoped>
$scale: v-bind(scale);
$green: #98d8aa;
$white: #fefefe;

$width-xl: calc(2500px / $scale);
$height-xl: calc(1686px / $scale);

$icon-bg-green: $green;
$icon-bg-white: $white;
$icon-font-color: $white;
$icon-border-color: darken($green, 20);
$icon-border-width: 3px;

.container {
  width: 100%;
  padding: 0 15px;
}

ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

.richmenu {
  width: $width-xl;
  height: $height-xl;
  display: flex;
  flex-wrap: wrap;
  border-width: $icon-border-width 0 0 $icon-border-width;
  border-style: solid;
  border-color: $icon-border-color;
  > li {
    border-width: 0 $icon-border-width $icon-border-width 0;
    border-style: solid;
    border-color: $icon-border-color;
  }
}

.icon {
  width: calc(100% / 3);
  height: calc($height-xl / 2);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  font-weight: bold;
  font-size: 2rem;
  &--green {
    background-color: $icon-bg-green;
    color: $icon-font-color;
  }
  &--white {
    background-color: $icon-bg-white;
    color: $green;
  }
  &__text {
    margin-top: 0.75rem;
    font-size: 1.5rem;
  }
}

.mt-3 {
  margin-top: 1rem;
}
</style>
