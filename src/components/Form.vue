<script setup>
import { ref } from "vue";

const nombre = ref("");
const fecha = ref("");
const tema = ref("");
const descripcion = ref("");
const mensaje = ref("");

const enviarSolicitud = async (event) => {
  event.preventDefault();

  const datosFormulario = {
    nombre: nombre.value,
    fecha: fecha.value,
    tema: tema.value,
    descripcion: descripcion.value,
  };

  try {
    const respuesta = await fetch("http://localhost:8080/api/v1/consult", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        name: datosFormulario.nombre,
        dateConsult: datosFormulario.fecha,
        typeConsult: datosFormulario.tema,
        description: datosFormulario.descripcion,
      }),
    });

    let datos;
    const contentType = respuesta.headers.get("content-type");

    if (contentType && contentType.includes("application/json")) {
      datos = await respuesta.json();
    } else {
      datos = {};
    }

    if (!respuesta.ok) {
      console.error("Error details:", datos);
      throw new Error(
        `Error al enviar la solicitud: ${
          datos.message || respuesta.statusText || "Unknown error"
        }`
      );
    }

    mensaje.value = "Solicitud enviada con éxito";
  } catch (error) {
    console.error("Fetch error:", error);
    mensaje.value = `Error: ${error.message}`;
  }
};
</script>

<template>
  <main>
    <div class="container mt-5">
      <div class="card">
        <div class="card-body">
          <form @submit="enviarSolicitud">
            <div class="form-group">
              <label for="nombre">Nombre de la Persona</label>
              <input
                type="text"
                class="form-control"
                id="nombre"
                v-model="nombre"
                placeholder="Ingrese su nombre"
              />
            </div>

            <div class="form-group">
              <label for="fecha">Fecha de la Solicitud</label>
              <input
                type="date"
                class="form-control"
                id="fecha"
                v-model="fecha"
              />
            </div>

            <div class="form-group">
              <label for="tema">Tema de la Consulta</label>
              <select class="form-control" id="tema" v-model="tema">
                <option value="" disabled>Seleccione un tema</option>
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
                class="form-control"
                id="descripcion"
                rows="4"
                v-model="descripcion"
                placeholder="Describa su consulta aquí"
              ></textarea>
            </div>
            <div id="containerbutton">
              <button type="submit" id="button" class="btn btn-primary">
                Enviar solicitud
              </button>
            </div>
          </form>
          <div
            v-if="mensaje"
            class="alert mt-3"
            :class="{
              'alert-success': mensaje.includes('éxito'),
              'alert-danger': mensaje.includes('Error'),
            }"
          >
            {{ mensaje }}
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
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
.alert {
  padding: 10px;
  border-radius: 5px;
}
.alert-success {
  background-color: #d4edda;
  color: #155724;
}
.alert-danger {
  background-color: #f8d7da;
  color: #721c24;
}
</style>
