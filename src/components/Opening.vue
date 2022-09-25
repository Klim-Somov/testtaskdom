<template>
  <form>
    <input
      @change="onPush(openingsSquare)"
      v-model.number="openingsSquare"
      type="text"
      placeholder="4.5"
    />
  </form>
</template>

<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "Opening",
  props: ["onPush"],
  setup() {
    const openingsSquare = ref();
    return { openingsSquare };
  },
});
</script>
<style scoped>
input {
  border:none;
}
</style>