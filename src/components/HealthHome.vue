<script setup></script>
<template>
  <main>
    <img src="../assets/health.png" alt="" />
  </main>
</template>
<style scoped>
main {
  width: 50%;

  height: 750px;
  display: flex;
  justify-content: center;
  align-items: center;
}
img {
  width: 800px;
}
@media (max-width: 768px) {
  main {
    height: 400px;
  }
  img {
    width: 300px;
  }
}
</style>
