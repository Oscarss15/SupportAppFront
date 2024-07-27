<script setup></script>
<template>
  <main>
    <div class="container mt-5">
      <div class="card">
        <div class="card-body">
          <form>
            <div class="form-group">
              <label for="nombre">Nombre de la Persona</label>
              <input
                type="text"
                class="form-control"
                id="nombre"
                placeholder="Ingrese su nombre"
              />
            </div>

            <div class="form-group">
              <label for="fecha">Fecha de la Solicitud</label>
              <input type="date" class="form-control" id="fecha" />
            </div>

            <div class="form-group">
              <label for="tema">Tema de la Consulta</label>
              <select class="form-control" id="tema">
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
                class="form-control"
                id="descripcion"
                rows="4"
                placeholder="Describa su consulta aquí"
              ></textarea>
            </div>
            <div id="containerbutton">
              <button type="submit" id="button" class="btn btn-primary">
                Enviar solicitud
              </button>
            </div>
          </form>
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
</style>
