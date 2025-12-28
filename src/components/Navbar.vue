<template>
  <nav class="navbar navbar-expand-lg navbar-light fixed-top">
    <div class="container-fluid">
      <img class="logo" src="@/assets/img/logo.svg" alt="logo" />

      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav mx-auto">
          <li class="nav-item" v-for="s in slides" :key="s.id" @click="go(s.id)">
                <a class="nav-link">{{ s.title }}</a> 
            </li>
        </ul>

        <button class="theme-toggle-btn" @click="toggleTheme">
          <span v-if="theme === 'light'">🌙 Dark</span>
          <span v-else>☀️ Light</span>
        </button>
      </div>
    </div>
  </nav>
</template>

<script setup>
    import { ref, onMounted } from "vue";

    const theme = ref("light");

    // 初始讀取使用者偏好
    onMounted(() => {
      const saved = localStorage.getItem("theme");
      if (saved) {
        theme.value = saved;
        document.documentElement.setAttribute("data-theme", saved);
      }
    });

    function toggleTheme() {
      theme.value = theme.value === "light" ? "dark" : "light";
      document.documentElement.setAttribute("data-theme", theme.value);
      localStorage.setItem("theme", theme.value);
    }

    const props = defineProps({
        slides: Array
    });

    const emit = defineEmits(["go-section"]);

    function go(id) {
        emit("go-section", id);
    }
</script>

<style scoped src="@/assets/styles/navbar.scss"></style>
