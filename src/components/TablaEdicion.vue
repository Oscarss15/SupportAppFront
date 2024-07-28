<script setup>
import { ref, onMounted } from "vue";

const solicitudes = ref([]);
const selectedSolicitud = ref(null);
const editForm = ref({
  name: "",
  dateConsult: "",
  typeConsult: "",
  description: "",
});

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

const deleteSolicitud = async (idConsult) => {
  try {
    const response = await fetch(
      `http://localhost:8080/api/v1/consult/${idConsult}`,
      {
        method: "DELETE",
      }
    );
    if (!response.ok) {
      throw new Error("Network response was not ok");
    }

    solicitudes.value = solicitudes.value.filter(
      (solicitud) => solicitud.idConsult !== idConsult
    );
  } catch (error) {
    console.error("Error deleting solicitud:", error);
  }
};

const openEditModal = (solicitud) => {
  selectedSolicitud.value = solicitud;
  editForm.value = {
    name: solicitud.name,
    dateConsult: solicitud.dateConsult.join("-"),
    typeConsult: solicitud.typeConsult,
    description: solicitud.description,
  };
};

const updateSolicitud = async () => {
  try {
    const response = await fetch(
      `http://localhost:8080/api/v1/consult/${selectedSolicitud.value.idConsult}`,
      {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(editForm.value),
      }
    );
    if (!response.ok) {
      throw new Error("Network response was not ok");
    }
    const updatedSolicitud = await response.json();
    const index = solicitudes.value.findIndex(
      (solicitud) => solicitud.idConsult === updatedSolicitud.idConsult
    );
    solicitudes.value[index] = updatedSolicitud;
  } catch (error) {
    console.error("Error updating solicitud:", error);
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
          <th scope="col">Editar</th>
          <th scope="col">Eliminar</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="solicitud in solicitudes" :key="solicitud.idConsult">
          <td>{{ solicitud.name }}</td>
          <td>{{ solicitud.dateConsult.join("-") }}</td>
          <td>{{ solicitud.typeConsult }}</td>
          <td>{{ solicitud.description }}</td>
          <td>
            <img
              src="../assets/edicionfinal.png"
              alt="Editar"
              data-bs-toggle="modal"
              data-bs-target="#exampleModal"
              @click="openEditModal(solicitud)"
            />
          </td>
          <td>
            <img
              src="../assets/eliminarfinal.png"
              alt="Eliminar"
              @click="deleteSolicitud(solicitud.idConsult)"
            />
          </td>
        </tr>
      </tbody>
    </table>

    <!-- Modal -->
    <div
      class="modal fade"
      id="exampleModal"
      tabindex="-1"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Editar Consulta</h5>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>

          <div class="container mt-5">
            <div class="card">
              <div class="card-body">
                <form @submit.prevent="updateSolicitud">
                  <div class="form-group">
                    <label for="nombre">Nombre de la Persona</label>
                    <input
                      v-model="editForm.name"
                      type="text"
                      class="form-control"
                      id="nombre"
                      placeholder="Ingrese su nombre"
                    />
                  </div>

                  <div class="form-group">
                    <label for="fecha">Fecha de la Solicitud</label>
                    <input
                      v-model="editForm.dateConsult"
                      type="date"
                      class="form-control"
                      id="fecha"
                    />
                  </div>

                  <div class="form-group">
                    <label for="tema">Tema de la Consulta</label>
                    <select
                      v-model="editForm.typeConsult"
                      class="form-control"
                      id="tema"
                    >
                      <option>Seleccione un tema</option>
                      <option>Cirugía</option>
                      <option>Dermatología</option>
                      <option>Neurología</option>
                      <option>Oftalmología</option>
                      <option>Pediatría</option>
                      <option>Traumatología</option>
                    </select>
                  </div>

                  <div class="form-group">
                    <label for="descripcion">Descripción de la Consulta</label>
                    <textarea
                      v-model="editForm.description"
                      class="form-control"
                      id="descripcion"
                      rows="4"
                      placeholder="Describa su consulta aquí"
                    ></textarea>
                  </div>
                  <div id="containerbutton">
                    <button type="submit" id="button" class="btn btn-primary">
                      Guardar cambios
                    </button>
                  </div>
                </form>
              </div>
            </div>
          </div>

          <div class="modal-footer">
            <button
              type="button"
              id="buttonsecondary"
              class="btn btn-secondary"
              data-bs-dismiss="modal"
            >
              Cerrar
            </button>
          </div>
        </div>
      </div>
    </div>
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

main {
  padding: 20px;
}
.card {
  background-color: #a52e22;
  border-radius: 10px;
}
select,
textarea,
input {
  background-color: #fae1e1;
}
label {
  color: white;
}
.form-group {
  padding: 10px;
}
#button {
  background-color: #fae1e1;
  color: black;
  border: 2px solid #fae1e1;
  text-align: center;
}
#button:hover {
  background-color: #a52e22;
  color: white;
}
#containerbutton {
  text-align: center;
  margin: 10px;
}
option {
  background-color: #fae1e1;
}

#buttonsecondary {
  background-color: #a52e22;
  color: white;
  border: 2px solid #fae1e1;
  text-align: center;
}
#buttonsecondary:hover {
  background-color: #fae1e1;
  border: 2px solid #a52e22;
  color: black;
}
</style>
