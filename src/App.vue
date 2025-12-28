<template>
  <Navbar :slides="slides" @go-section="scrollToSection" />
  <FullpageWrapper :slides="slides" ref="fullpageRef" />
</template>

<script setup>
import { ref } from 'vue'
import Navbar from '@/components/Navbar.vue'
import FullpageWrapper from '@/components/FullpageWrapper.vue'

const slides = [
  {
    id: 'slide1',
    title: 'Taipei',
    bg: 'src/assets/img/bg1.jpg',
    intro: '台灣的政治與文化中心，融合現代都市感與多元藝文氣息。',
  },
  {
    id: 'slide2',
    title: 'NewTaipei',
    bg: 'src/assets/img/bg2.jpg',
    intro: '環繞台北的廣闊都會圈，擁有山海河港的多元景觀。',
  },
  {
    id: 'slide3',
    title: 'Taoyuan',
    bg: 'src/assets/img/bg3.jpg',
    intro: '國門所在的新興科技城，交通與產業發展迅速。',
  },
  {
    id: 'slide4',
    title: 'Taichung',
    bg: 'src/assets/img/bg4.jpg',
    intro: '氣候宜人、生活步調舒適，被譽為最適合居住的城市之一。',
  },
  {
    id: 'slide5',
    title: 'Tainan',
    bg: 'src/assets/img/bg5.jpg',
    intro: '台灣最古老的城市，以深厚歷史、文化底蘊與美食著名。',
  },
  {
    id: 'slide6',
    title: 'Kaohsiung',
    bg: 'src/assets/img/bg6.jpg',
    intro: '南台灣的海港大城，兼具現代化建設與海洋城市魅力。',
  },
]

const fullpageRef = ref(null)

function scrollToSection(id) {
  fullpageRef.value?.goToSection(id)
}
</script>
