<script setup></script>
<template>
  <main>
    <table class="table table-striped">
      <thead>
        <tr>
          <th scope="col">Id</th>
          <th scope="col">Nombre Solicitante</th>
          <th scope="col">Fecha solicitud</th>
          <th scope="col">Tema consulta</th>
          <th scope="col">Descripcion consulta</th>
          <th scope="col">Editar</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th scope="row">1</th>
          <td>Maria</td>
          <td>10/12/2023</td>
          <td>Pediatria</td>
          <td>Descripcion1</td>
          <td><img src="../assets/edicion.png" alt="" /></td>
        </tr>
        <tr>
          <th scope="row">2</th>
          <td>Maria</td>
          <td>10/12/2023</td>
          <td>Digestivo</td>
          <td>Descripcion1</td>
          <td><img src="../assets/edicion.png" alt="" /></td>
        </tr>
        <tr>
          <th scope="row">3</th>
          <td>Maria</td>
          <td>10/12/2023</td>
          <td>Recuperacion</td>
          <td>Descripcion1</td>
          <td><img src="../assets/edicion.png" alt="" /></td>
        </tr>
        <tr>
          <th scope="row">3</th>
          <td>Maria</td>
          <td>10/12/2023</td>
          <td>Recuperacion</td>
          <td>Descripcion1</td>
          <td><img src="../assets/edicion.png" alt="" /></td>
        </tr>
        <tr>
          <th scope="row">3</th>
          <td>Maria</td>
          <td>10/12/2023</td>
          <td>Recuperacion</td>
          <td>Descripcion1</td>
          <td><img src="../assets/edicion.png" alt="" /></td>
        </tr>
        <tr>
          <th scope="row">3</th>
          <td>Maria</td>
          <td>10/12/2023</td>
          <td>Recuperacion</td>
          <td>Descripcion1</td>
          <td><img src="../assets/edicion.png" alt="" /></td>
        </tr>
        <tr>
          <th scope="row">3</th>
          <td>Maria</td>
          <td>10/12/2023</td>
          <td>Recuperacion</td>
          <td>Descripcion1</td>
          <td><img src="../assets/edicion.png" alt="" /></td>
        </tr>
        <tr>
          <th scope="row">3</th>
          <td>Maria</td>
          <td>10/12/2023</td>
          <td>Recuperacion</td>
          <td>Descripcion1</td>
          <td><img src="../assets/edicion.png" alt="" /></td>
        </tr>
      </tbody>
    </table>
  </main>
</template>
<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
}
table {
  width: 70%;
  border-collapse: collapse;
}
th {
  background-color: #a52e22 !important;
  color: white;
}
tr {
  background-color: #a52e22 !important;
}
td {
  background-color: #d67979 !important;
}
img {
  width: 25px;
  height: 25px;
}
@media (max-width: 768px) {
  main {
    max-height: 800px;
    overflow-y: auto;
  }
  table,
  thead,
  tbody,
  th,
  td,
  tr {
    display: block;
  }

  thead tr {
    display: none;
  }

  tr {
    margin-bottom: 10px;
  }

  td {
    text-align: right;
    padding-left: 50%;
    position: relative;
  }

  td::before {
    content: attr(data-label);
    position: absolute;
    left: 0;
    width: 50%;
    padding-left: 10px;
    font-weight: bold;
    text-align: left;
  }
  table {
    margin-top: auto;
    padding-top: 20px;
  }
  img {
    filter: hue-rotate(30);
  }
}
</style>
