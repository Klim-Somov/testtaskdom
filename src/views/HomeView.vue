<template>
  <div class="home">
    <form action="расчитать">
      <p>введите высоту стены в метрах</p>
      <input v-model.number="wallWidth" placeholder="7" />
      <p>введите длинну стены в метрах</p>
      <input v-model.number="wallHeight" placeholder="2.5" />
    </form>
    <p>введите площадь проема</p>
    <Opening :onPush="onPush" v-for="(doors, index) in openings" :key="index" />
    <button @click="addDoor">добавить проем</button>
  </div>
  <div>
    <button @click="calculateOutcome">расчитать количество блоков</button>
  </div>
  <div v-if="outcomeSum">
    блоков для постройки перегородки потребуется: {{ outcomeSum }} шт.
  </div>
  <div v-else-if="outcomeSum < 0">"кажется ошибка в измерении проема"</div>
  <div v-if="outcomeWeight">общий вес плит: {{ outcomeWeight }} кг.</div>
</template>

<script>
import { defineComponent, ref } from "vue";
import Opening from "../components/Opening.vue";

export default defineComponent({
  name: "HomeView",
  components: { Opening },

  setup() {
    const openings = ref(new Array(1));

    const addDoor = () => {
      openings.value.push(1);
    };
    const arr = [];
    const onPush = (item) => {
      openingsSquare.value += item;
      console.log(openingsSquare);
    };
    const wallWidth = ref();
    const wallHeight = ref();
    const openingsSquare = ref(null);
    const outcomeSum = ref();
    const outcomeWeight = ref();
    const calculateOutcome = () => {
      const result = Math.ceil(
        (wallWidth.value * wallHeight.value) / 0.3335 - openingsSquare.value
      );
      result < 0 ? (outcomeSum.value = "") : (outcomeSum.value = result);
      outcomeWeight.value = outcomeSum.value * 36;
    };

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
