<template>
  <button class="button">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "MainButton",
  props: ["text"],
};
</script>
<style scoped>
.button {
  margin-top: 8px;
  background: #4bd765;
  border-radius: 24px;
  border: none;
  padding: 8px 30px;
  height: 36px;
  font-weight: 500;
  text-align: center;
  cursor: pointer;
  color: #ffffff;
}
</style>
