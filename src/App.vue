<template>
  <div class="content">
    <h1>Калькулятор Пазогребневых Гипсовах Плит</h1>
    <form class="form">
      <p>введите высоту стены в метрах</p>
      <input v-model.number="wallWidth" placeholder="7" />
      <p>введите длинну стены в метрах</p>
      <input v-model.number="wallHeight" placeholder="2.5" />
    </form>
    <div class="opening">
      <p>введите площадь проема в м²</p>
      <Opening
        :onPush="onPush"
        v-for="(doors, index) in openings"
        :key="index"
      />
      <MainButton @click="addDoor" text="добавить проем" />
    </div>
    <div>
      <MainButton
        @click="calculateOutcome"
        text="расчитать количество блоков"
      />
    </div>
    <div v-if="outcomeSum">
      блоков для постройки перегородки потребуется: {{ outcomeSum }} шт.
    </div>
    <div v-else-if="outcomeSum > 0">кажется ошибка в измерении проема</div>
    <div v-if="outcomeWeight">общий вес плит: {{ outcomeWeight }} кг.</div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import Opening from "@/components/Opening.vue";
import MainButton from "@/components/MainButton.vue";

export default defineComponent({
  name: "HomeView",
  components: { Opening, MainButton },

  setup() {
    const openings = ref(new Array(1));

    function addDoor() {
      openings.value.push(1);
    }
    function onPush(item: number) {
      openingsSquare.value += item;
    }
    const wallWidth = ref();
    const wallHeight = ref();
    const openingsSquare = ref(0);
    const outcomeSum = ref();
    const outcomeWeight = ref();
    function calculateOutcome() {
      const result = Math.ceil(
        (wallWidth.value * wallHeight.value) / 0.3335 - openingsSquare.value
      );
      result < 0 ? (outcomeSum.value = "") : (outcomeSum.value = result);
      outcomeWeight.value = outcomeSum.value * 36;
    }

    return {
      openings,
      addDoor,
      wallWidth,
      wallHeight,
      openingsSquare,
      calculateOutcome,
      outcomeSum,
      outcomeWeight,
      onPush,
    };
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #38495a;
}
body {
  font-size: 20px;
  background-color: rgb(143, 165, 189);
}
.content {
  padding-bottom: 20px;
  padding: 10px;
  background-color: rgb(217, 235, 235);
  max-width: 600px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 10px;
  align-items: center;
  min-height: 100vh;
  border-radius: 20px;
}
.form > input {
  background-color: rgb(247, 247, 247);
  border: none;
  border-radius: 15px;
  padding: 8px;
}
.opening {
  background-color: rgba(59, 59, 60, 0.4);
  border: none;
  border-radius: 15px;
  padding: 20px;
}
.opening > input {
  border: none;
}
</style>
