<template>
  <div class="container">
    <div class="timer">
      <h1>
        {{ stopWatch }}
      </h1>
      <button class="button bold" @click="startTimer()">PLAY</button>
      <button class="button bold" @click="pauseTimer()">PAUSE</button>
      <div class="aa">
        <div class="skill php">60%</div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "@vue/reactivity";
export default {
  name: "App",
  components: {},
  setup() {
    const timer = ref(25);
    const seconds = ref(59);

    let stopWatch = ref(`${timer.value}:${seconds.value}`);
    let stopwatchRef = null;

    const startTimer = async () => {
      if (!stopwatchRef) {
        timer.value--;
      }
      stopwatchRef = setInterval(async () => {
        if (seconds.value == 0) {
          seconds.value = 59;
          timer.value--;
        } else {
          seconds.value--;
        }

        console.log(seconds.value.toString.length);
        stopWatch.value = `${timer.value}:${
          seconds.value > 9 ? seconds.value : "0" + seconds.value
        }`;
      }, 100);
    };

    const pauseTimer = async () => {
      clearInterval(stopwatchRef);
    };
    return { timer, stopWatch, startTimer, pauseTimer };
  },
};
</script>

<style>
@import "./assets/styles/variables.css";
@import "./assets/styles/base.css";

p {
  font-size: 20px;
}

.php {
  width: 60%;
}
.aa {
  background-color: rgb(192, 192, 192);
  width: 80%;
  border-radius: 15px;
}

.skill {
  background-color: rgb(116, 194, 92);
  color: white;
  padding: 1%;
  text-align: right;
  font-size: 20px;
  border-radius: 15px;
}

#app {
  font-family: Montserrat;
  background: var(--grey);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 60px;
}
</style>
