<template>
  <Navbar :slides="slides" @go-section="scrollToSection" />
  <FullpageWrapper :slides="slides" ref="fullpageRef" />
</template>

<script setup>
import { ref } from 'vue'
import Navbar from '@/components/Navbar.vue'
import FullpageWrapper from '@/components/FullpageWrapper.vue'
import bg1 from '@/assets/img/bg1.jpg'
import bg2 from '@/assets/img/bg2.jpg'
import bg3 from '@/assets/img/bg3.jpg'
import bg4 from '@/assets/img/bg4.jpg'
import bg5 from '@/assets/img/bg5.jpg'
import bg6 from '@/assets/img/bg6.jpg'

const slides = [
  {
    id: 'slide1',
    title: 'Taipei',
    bg: bg1,
    intro: '台灣的政治與文化中心，融合現代都市感與多元藝文氣息。',
  },
  {
    id: 'slide2',
    title: 'NewTaipei',
    bg: bg2,
    intro: '環繞台北的廣闊都會圈，擁有山海河港的多元景觀。',
  },
  {
    id: 'slide3',
    title: 'Taoyuan',
    bg: bg3,
    intro: '國門所在的新興科技城，交通與產業發展迅速。',
  },
  {
    id: 'slide4',
    title: 'Taichung',
    bg: bg4,
    intro: '氣候宜人、生活步調舒適，被譽為最適合居住的城市之一。',
  },
  {
    id: 'slide5',
    title: 'Tainan',
    bg: bg5,
    intro: '台灣最古老的城市，以深厚歷史、文化底蘊與美食著名。',
  },
  {
    id: 'slide6',
    title: 'Kaohsiung',
    bg: bg6,
    intro: '南台灣的海港大城，兼具現代化建設與海洋城市魅力。',
  },
]

const fullpageRef = ref(null)

function scrollToSection(id) {
  fullpageRef.value?.goToSection(id)
}
</script>
