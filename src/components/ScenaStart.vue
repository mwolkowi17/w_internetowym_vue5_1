<script setup>
import { ref } from 'vue'

const emit = defineEmits(['koniec-planszy', 'instrukcja-focus']) //dodanie emitera eventu z klawiatury

const props = defineProps({
  ifButtonOnFocus: Boolean
})
const stageParent = ref(null)

//nieużywana funkcja fullscreen - to obsługuje platforma
function openFullscreen() {
  console.log("openFullscreen called");

  const element = stageParent.value;
  console.log("Element to fullscreen:", element);
  if (element && element.requestFullscreen) {
    element.requestFullscreen().catch((error) => {
      console.log(error.message);
    });
  } else {
    console.log('Fullscreen API not supported or ref not found');
  }
}
</script>

<template>
  <div ref="stageParent" class="tlo" role="img" alt="plansza startu gry" aria-label="W internetowym labiryncie">
  </div>
  <button class="start my-button" @click="$emit('koniec-planszy')" @keydown.enter="$emit('instrukcja-focus')"
    role="button">START</button>
</template>

<style scoped>
.tytul {
  color: greenyellow;
}

.tlo {
  background-image: url("../assets/plansza_start.png");
  background-size: 1920px 1080px;
  height: 1080px;
  width: 1920px;
  top: 0px;
  left: 0px;
  position: absolute;
}

.start {
  color: rgb(29, 56, 80);
  font-size: 100px;
  font-style: bold;
  font-weight: 700;
  font-family: "Proxima Nova", sans-serif;
  background-size: 432px 168px;
  background-position: -2px -3px;
  background-repeat: no-repeat;
  position: absolute;
  top: 600px;
  left: 720px;
  width: 432px;
  height: 168px;
  border: 4px solid rgb(0, 187, 255);
  /*transition: .2s ease-out;*/
  overflow: visible;

}


/* .start:hover::after{
   content: '';
  position: absolute;
  left: 0;
  top: 0;
  margin-left:10px;
  margin-top:-10px;
  height: 130%;
  width: 110%;
  border: 3px solid blue;
  box-sizing: border-box;
  padding:10px;
} */



.start:focus {
  outline: 5px solid #08e926;
  /* outline: 8px solid #9a009e; */
  /* outline: thick double #08e926; */
}
</style>