<script setup></script>
<template>
  <main>
    <content>
      <h2>Consulta</h2>
      <h2>Medica</h2>
      <h2>Online</h2>
    </content>
  </main>
</template>
<style scoped>
h2 {
  color: #a52e22;
  font-size: 120px;
  display: flex;
  justify-content: center;
  align-items: center;
}
main {
  width: 50%;
  height: 750px;
  display: flex;
  justify-content: center;
  align-items: center;
}
@media (max-width: 768px) {
  main {
    width: 100%;
    height: 400px;
  }
  h2 {
    font-size: 80px;
  }
}
</style>
