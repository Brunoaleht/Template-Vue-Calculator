<template>
  <div class="display">{{ value }}</div>
</template>

<script>
export default {
  name: "DisplayCalc",
  props: { value: { type: Array } },
};
</script>

<style>
.display {
  grid-column: span 4;
  background-color: #0004;

  display: flex;
  justify-content: flex-end;
  align-items: center;
  padding: 20px;
  font-size: 2.2em;
  overflow: hidden;
}
</style>
