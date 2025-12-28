<template>
  <section class="section" :id="slideId" :style="bgStyle">
    <div class="container">
      <div class="row">
        <div class="col-md-12 w-full">
          <div class="upper text-center">
            <h2>{{ title }}</h2>
            <p>{{ intro }}</p>
          </div>
        </div>
      </div>
    </div>
    <div class="lower text-center">
        <div>
            <a class="btn1" href="">OFFICIAL WEBSITE</a>
            <a class="btn2" href="">LANDSCAPE PHOTOS</a>
        </div>
        <div>
            <a class="arrow" href="">
            <svg width="24" height="24" xmlns="http://www.w3.org/2000/svg">
                <path
                d="M23.245 4l-11.245 14.374-11.219-14.374-.781.619 12 15.381 12-15.391-.755-.609z"
                />
            </svg>
            </a>
        </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { computed } from "vue";

const props = defineProps({
  slideId: String,
  bg: String,
  title: String,
  intro: String
});

const bgStyle = computed(() => ({
  backgroundImage: `url(${props.bg})`,
  backgroundSize: "cover",
  backgroundPosition: "center",
}));
</script>

<style scoped src="@/assets/styles/slide.scss"></style>
