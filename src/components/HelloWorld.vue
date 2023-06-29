<template>
  <div :class="{'dark-mode': isDarkMode}">
    <button @click="toggleMode" class="btn btn-primary">
      {{ isDarkMode ? 'Light Mode' : 'Dark Mode' }}
    </button>
  </div>
</template>
<script>
export default {
  data() {
    return {
      isDarkMode: false
    };
  },
  created() {
    // Check if the user has a preferred mode stored
    const preferredMode = localStorage.getItem('preferredMode');
    if (preferredMode) {
      this.isDarkMode = preferredMode === 'dark';
    } else {
      // Use system preference if available
      this.isDarkMode = window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches;
    }
  },
  methods: {
    toggleMode() {
      this.isDarkMode = !this.isDarkMode;
      localStorage.setItem('preferredMode', this.isDarkMode ? 'dark' : 'light');
    }
  }
};
</script>

<style>
body {
  transition: background-color 0.3s, color 0.3s;
}

.dark-mode {
  background-color: #333;
  color: #fff;
}
</style>