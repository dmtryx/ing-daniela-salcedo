<script setup>
import { ref, onMounted, onUnmounted } from "vue";
const class_container = ref("landing-section");
const url_img = ref("/src/assets/landing_house.png");

const props = defineProps({
  proyecto: String,
  titulo: String,
  descripcion: String,
});

const detectScreen = () => {
  if (window.innerWidth < 620) {
    class_container.value = "landing-section-mb";
    url_img.value = "/src/assets/saa.png";
    console.log("cambia");
  } else {
    class_container.value = "landing-section";
    url_img.value = "/src/assets/landing_house.png";
  }
};

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
  <div :class="class_container">
    <div class="info">
      <h1>{{ titulo }}</h1>
      <p>
        {{ descripcion }}
      </p>
      <div class="butttons-div">
        <button class="btn btn-warning" type="button">Solicitar cita</button>
        <button class="btn btn-outline-warning" type="button">
          Descargar portafolio
        </button>
      </div>
    </div>
    <div class="img-div">
      <img :src="url_img" alt="olaaaaa" />
    </div>
  </div>
</template>

<style lang="scss">
.landing-section {
  padding: 0 3rem;
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  height: 100vh;
  justify-content: space-around;
  align-items: center;
  width: 100%;
  //max-width: 1300px;

  /*animation: cambio-color 5s infinite;  5 segundos de duración para cada cambio, se repite infinitamente */

  .info {
    padding-top: 0rem;
    max-width: 600px;
    margin: 5rem 0;

    h1 {
      font-size: 2.5rem;
      font-weight: bold;
      line-height: normal;
      margin-bottom: 2rem;
    }

    .butttons-div {
      display: flex;
      flex-wrap: wrap;
      justify-content: start;
      gap: 1rem;

      button {
        margin-bottom: 1rem;
      }
    }
  }

  .img-div {
    padding-top: 0rem;
    img {
      width: 100%;
      max-width: 800px;
      height: auto;
      margin-bottom: -3rem;
    }
  }
}

.landing-section-mb {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  height: 100vh;
  justify-content: center;
  align-items: center;
  width: 100%;
  position: relative;
  background-image: url("@/assets/saa.png");
  background-repeat: no-repeat;
  background-position: center bottom;
  background-size: contain; /* Esto hace que la imagen cubra todo el contenedor */
  background-color: #111c29;
  gap: 1rem;

  .info {
    max-width: 400px;
    display: flex;
    flex-direction: column;
    color: white;
    height: 100%;
    padding: 7rem 10% 7rem 10%;

    h1 {
      font-size: 2rem;
      font-weight: bolder;
      line-height: normal;
      margin-bottom: 1rem;
      line-height: 90%;
    }

    .butttons-div {
      display: flex;
      flex-wrap: wrap;
      justify-content: start;
      gap: 1rem;
      margin-top: 1rem;

      button {
        margin-bottom: 1rem;
        backdrop-filter: blur(3px);
      }
    }
  }

  .img-div {
    display: none;
    img {
      width: 100%;
      max-width: 600px;
      height: auto;
    }
  }
}

@keyframes cambio-color {
  0% {
    background-color: red;
  }
  50% {
    background-color: blue;
  }
  100% {
    background-color: blue;
  }
  /*
    0% {
        background: linear-gradient(to bottom right, red, blue);
    }
    50% {
        background: linear-gradient(to bottom right, blue, red);
    }
    100% {
        background: linear-gradient(to bottom right, red, blue);
    }
    */
}
</style>
