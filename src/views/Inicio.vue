<script setup>
import ProjectCards from "@/components/ProjectCards.vue";
import LandingPage from "@/components/LandingPage.vue";

import { ref, onMounted, onUnmounted } from "vue";
const con_res = ref("info isnt_mobile");
const hide_hr = ref(true);

const detectScreen = () => {
  if (window.innerWidth < 1050) {
    con_res.value = "info is_mobile";
  } else {
    con_res.value = "info isnt_mobile";
  }

  if (window.innerWidth < 620) {
    hide_hr.value = false;
  } else {
    hide_hr.value = true;
  }
};

const titulo = ref("");
const descripcion = ref("");
const seccion_1 = ref([]);
const seccion_2 = ref([]);
const seccion_3 = ref([]);
const seccion_4 = ref([]);
const seccion_5 = ref([]);

const fetchData = async () => {
  try {
    const response = await fetch("data.json");
    const data = await response.json();
    titulo.value = data.titulo;
    descripcion.value = data.descripcion;
    seccion_1.value = data.seccion_1;
    seccion_2.value = data.seccion_2;
    seccion_3.value = data.seccion_3;
    seccion_4.value = data.seccion_4;
    seccion_5.value = data.seccion_5;
  } catch (error) {
    console.error("Error al cargar los datos:", error);
  }
};

onMounted(fetchData);

try {
  // Registra el evento 'resize' al montar el componente para detectar cambios en la resolución
  onMounted(() => {
    detectScreen();
    window.addEventListener("resize", detectScreen);
  });

  // Asegúrate de quitar el evento 'resize' cuando el componente se destruye para evitar fugas de memoria
  onUnmounted(() => {
    window.removeEventListener("resize", detectScreen);
  });
} catch (err) {
  console.log(err);
}
</script>
<template>
  <div class="inicio-container">
    <LandingPage :titulo="titulo" :descripcion="descripcion" />
    <hr v-if="hide_hr" />
    <div class="services-section">
      <div class="container-cards">
        <div
          class="item"
          v-for="seccion_obj in seccion_1"
          :key="seccion_obj.servicio"
        >
          <img :src="seccion_obj.icono" alt="" />
          <h3>{{ seccion_obj.servicio }}</h3>
          <p>{{ seccion_obj.descripcion }}</p>
        </div>
      </div>
    </div>
    <hr />
    <div class="proyectos-container">
      <h2>Trabajos recientes</h2>
      <ProjectCards
        v-for="seccion_obj in seccion_2"
        :key="seccion_obj.proyecto"
        :proyecto="seccion_obj.proyecto"
        :imglink="seccion_obj.imglink"
        :fecha="seccion_obj.fecha"
        :tipo="seccion_obj.tipo"
        :supervisor="seccion_obj.supervisor"
        :contratista="seccion_obj.contratista"
      />
      <button class="btn btn-warning mt-3" type="button">
        Ver mas trabajos
      </button>
    </div>
    <hr />
    <div class="sobre-mi-section">
      <div class="cont-im">
        <img
          src="https://d5tnfl9agh5vb.cloudfront.net/uploads/2020/04/foto_christa_mina.jpg"
          alt="foto dani"
        />
      </div>
      <div class="info">
        <h2>Sobre Mí</h2>
        <p v-for="(parrafo, index) in seccion_3" :key="index">
          {{ parrafo }}
        </p>
      </div>
    </div>
    <div class="clientes-section">
      <h2>{{ seccion_4.titulo }}</h2>
      <div class="opinion-container">
        <div
          class="card-op"
          v-for="(opinion, index) in seccion_4.opiniones"
          :key="index"
        >
          <p>
            {{ opinion.opinion }}
          </p>
          <hr />
          <div class="info-card">
            <img :src="opinion.imagen" alt="imgane person" />

            <div class="card-text">
              <h3>{{ opinion.nombre }}</h3>
              <p>{{ opinion.entidad }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <hr />
    <div class="contacto-section">
      <h2>{{seccion_5.titulo}}</h2>
      <div class="container">
        <div :class="con_res">
          <div>
            <p>
              {{seccion_5.descripcion}}
            </p>
            <div class="d-flex cont">
              <span class="mdi mdi-email-outline" style="color: #ffc107"></span>
              <p>dfernanda.salcedo24@gmail.com</p>
            </div>
            <div class="d-flex cont">
              <a href="https://wa.me/+573157313902">
                <span
                  class="mdi mdi-whatsapp"
                  style="color: #008a55; font-size: large"
                ></span>
                <p>+57 315 7313902</p>
              </a>
            </div>
          </div>
          <img :src="seccion_5.imagen" alt="" />
        </div>
        <form class="form">
          <div class="mb-1">
            <label for="exampleFormControlTextarea1" class="form-label"
              >Nombre</label
            >
            <input
              type="text"
              placeholder="Nombre"
              class="form-control input-form"
              id="exampleInputEmail1"
              aria-describedby="emailHelp"
              required
            />
          </div>
          <div class="mb-1">
            <label for="exampleFormControlTextarea1" class="form-label"
              >Correo</label
            >
            <input
              type="email"
              placeholder="Correo"
              class="form-control input-form"
              id="exampleInputEmail1"
              aria-describedby="emailHelp"
              required
            />
          </div>
          <div class="mb-1">
            <label for="exampleFormControlTextarea1" class="form-label"
              >Celular</label
            >
            <input
              type="number"
              placeholder="Celular"
              class="form-control input-form"
              id="exampleInputEmail1"
              aria-describedby="emailHelp"
              required
            />
          </div>
          <div class="mb-1">
            <label for="exampleFormControlTextarea1" class="form-label"
              >Mensaje</label
            >
            <textarea
              class="form-control input-form mb-3"
              placeholder="Mensaje"
              id="exampleFormControlTextarea1"
              required
              rows="3"
            ></textarea>
          </div>
          <button type="submit" class="btn btn-warning">Submit</button>
        </form>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
@import "@/assets/styles/inicio.scss";
</style>
