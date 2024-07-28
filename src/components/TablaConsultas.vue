<script setup>
import { ref, onMounted } from "vue";

const solicitudes = ref([]);

const fetchSolicitudes = async () => {
  try {
    const response = await fetch("http://localhost:8080/api/v1/consult/all");
    if (!response.ok) {
      throw new Error("Network response was not ok");
    }
    const data = await response.json();
    console.log("Fetched data:", data);
    solicitudes.value = data;
  } catch (error) {
    console.error("Error fetching solicitudes:", error);
  }
};

onMounted(() => {
  fetchSolicitudes();
});
</script>

<template>
  <main>
    <table class="table table-striped">
      <thead>
        <tr>
          <th scope="col">Nombre Solicitante</th>
          <th scope="col">Fecha solicitud</th>
          <th scope="col">Tema consulta</th>
          <th scope="col">Descripción consulta</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="solicitud in solicitudes" :key="solicitud.idConsult">
          <td>{{ solicitud.name }}</td>
          <td>{{ solicitud.dateConsult.join("-") }}</td>
          <!-- Asumiendo que dateConsult es un array y quieres mostrarlo como una fecha -->
          <td>{{ solicitud.typeConsult }}</td>
          <td>{{ solicitud.description }}</td>
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
}
</style>
