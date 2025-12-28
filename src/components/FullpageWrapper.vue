<template>
  <div id="fullpage">
    <SlideSection
      v-for="(item, index) in slides"
      :key="item.id"
      :slide-id="item.id"
      :title="item.title"
      :bg="item.bg"
      :intro="item.intro"
    />
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from "vue";
import fullpage from "fullpage.js";
import "fullpage.js/dist/fullpage.css";
import { gsap } from "gsap";
import SlideSection from "./SlideSection.vue";

let fp: any = null;

const props = defineProps({
  slides: Array
});

defineExpose({
  goToSection
});

const activeIndex = ref(0);

function goToSection(id) {
  const index = props.slides.findIndex(s => s.id === id);
  if (index !== -1) fp.moveTo(index + 1);
}

function initFullpage() {
  // 如果已經初始化 → 先銷毀
  if (fp !== null) {
    try {
      fp.destroy("all"); // 🔥 必須加 all，不然 class 不會清乾淨
    } catch (e) {
      console.warn("Fullpage already destroyed");
    }
  }

  // 🔥 重新初始化
  fp = new fullpage("#fullpage", {
    licenseKey: "gplv3-license",
    autoScrolling: true,
    onLeave(origin, destination) {
        
      const section = destination.item; 
      const tl = gsap.timeline();

      tl
        .addLabel("power")
        .fromTo(
          section.querySelector(".upper"),
          { autoAlpha: 0 },
          { autoAlpha: 1, duration: 1.2, ease: "power2.out" },
          "power+=.5"
        )
        .fromTo(
          section.querySelector(".lower"),
          { autoAlpha: 0 },
          { autoAlpha: 1, duration: 1.2, ease: "power2.out" },
          "power+=1"
        );
        // if(fp.moveTo(2)) section.querySelector(".upper h2").css('color', 'white') 
    },
  });

  // 初始一次動畫
  const init = gsap.timeline();

  init
    .fromTo(
      ".upper h2",
      { autoAlpha: 0, y: 20 },
      { autoAlpha: 1, y: 0, duration: 1.2, ease: "power2.out" }
    )
    .addLabel("btns")
    .fromTo(
      ".upper p",
      { autoAlpha: 0 },
      { autoAlpha: 1, duration: 1.2, ease: "power2.out" },
      "btns"
    )
    .fromTo(
      ".btn1",
      { autoAlpha: 0, x: -20 },
      { autoAlpha: 1, x: 0, duration: 1.2, ease: "power2.out" },
      "btns"
    )
    .fromTo(
      ".btn2",
      { autoAlpha: 0, x: 20 },
      { autoAlpha: 1, x: 0, duration: 1.2, ease: "power2.out" },
      "btns"
    )
    .fromTo(".arrow", { autoAlpha: 0 }, { autoAlpha: 1 });
}

onMounted(() => {
  initFullpage();
});

// 🔥 離開元件時清除，避免回到此頁時 double init
onBeforeUnmount(() => {
  if (fp) {
    fp.destroy("all");
    fp = null;
  }
});
</script>
