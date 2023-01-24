<template>
  <div :class="Class" :id="Id">
    This is a component
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
  top: 10%;
  left: 30%;
}

</style>