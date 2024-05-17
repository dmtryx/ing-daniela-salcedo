<script setup>
const class_text = ref("/src/assets/text_white.png");
import { ref, onMounted, onUnmounted } from "vue";

const detectScreen = () => {
  if (window.innerWidth < 620) {
    class_text.value = "/src/assets/text_white.png";
  } else {
    class_text.value = "/src/assets/text_white.png";
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
    <nav>
        <div class="logo">
            <a><img class="a" src="@/assets/Logo3.png" alt=""></a>
            <img class="b" :src="class_text" style="width: 80%; max-width: 300px;" alt="">
        </div>
    </nav>
</template>

<style lang="scss">
nav {
    height: 4rem;
    display: flex;
    width: 100%;
    align-items: center;
    padding: 0 3rem;

    .logo {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100%;
        gap:1rem;
        

        a {
            display: flex;
            align-items: center;
            justify-content: center;

            .a {
                width: auto;
                height: 30px;
            }
        }

    }

    .links {
        display: flex;
    }

    .nav-link {
        color: white;
        /* Cambia este valor al color deseado */
        text-decoration: none;
        /* Quita el subrayado predeterminado */
        margin-right: 20px;
        /* Ajusta el espaciado entre los enlaces si es necesario */
    }

    /* Cambiar el color al pasar el cursor sobre los enlaces */
    .nav-link:hover {
        color: yellow;
        /* Cambia este valor al color deseado cuando se pasa el cursor */
    }

}
</style>
