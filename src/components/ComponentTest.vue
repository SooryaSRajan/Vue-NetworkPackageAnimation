<template>
  <div :class="Class" :id="Id">
    <h1>Some Computer</h1>
  </div>
</template>

<script>
export default {
  name: "ComponentTest",
  props: {
    Class: {
      type: String,
    },
    Id: {
      type: String,
    },
  },
}
</script>

<style scoped>
div {
  background-color: #2c3e50;
  padding: 10px;
  border-radius: 10px;
}

</style>