<script setup></script>
<template>
  <ul class="nav justify-content-center">
    <li class="nav-item">
      <RouterLink to="/"><a class="nav-link" href="#">Home</a></RouterLink>
    </li>
    <li class="nav-item">
      <RouterLink to="/formulario"
        ><a class="nav-link" href="#">Formulario</a></RouterLink
      >
    </li>
    <li class="nav-item">
      <RouterLink to="/consultas">
        <a class="nav-link" href="#">Consultas</a></RouterLink
      >
    </li>
    <li class="nav-item">
      <RouterLink to="/edicion">
        <a class="nav-link" href="#">Edición</a></RouterLink
      >
    </li>
  </ul>
</template>
<style scoped>
ul {
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #a52e22;
}
a {
  color: white;
  text-decoration: none;
}
a:hover {
  color: #df8989;
}
a:link,
:visited {
  color: #fff;
}
</style>
