<template>
  <main id="main">

    <NetworkInteractionComponent ref="childComponentRef">
      <ComponentTest class="box" id="box1"></ComponentTest>
      <ComponentTest class="box"></ComponentTest>
      <ComponentTest class="box"></ComponentTest>
      <ComponentTest class="box"></ComponentTest>
      <ComponentTest class="box" id="box6"></ComponentTest>
      <ComponentTest class="box"></ComponentTest>
      <ComponentTest class="box"></ComponentTest>
      <ComponentTest class="box"></ComponentTest>
      <ComponentTest class="box"></ComponentTest>
    </NetworkInteractionComponent>
  </main>
</template>

<script>
import NetworkInteractionComponent from "@/components/NetworkInteractionComponent";
import ComponentTest from "@/components/ComponentTest";

export default {
  name: 'App',
  mounted() {
    this.$refs.childComponentRef.setPackage("box1", "")
    this.$refs.childComponentRef.setPackage("box2", "")
    this.$refs.childComponentRef.setPackage("box3", "")
    this.$refs.childComponentRef.setPackage("box4", "")
    this.$refs.childComponentRef.setPackage("box5", "")
    this.$refs.childComponentRef.drawLine("box1", "box6")
    this.$refs.childComponentRef.animatePackage("box6")
  },
  data: function () {
    return {}
  },
  components: {ComponentTest, NetworkInteractionComponent},
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
}

main {
  height: 100vh;
  width: 100vw;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 0;
  padding: 0;
}
</style>

<style scoped>
.box {
  position: absolute;
  width: 50px;
  height: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: black;
  font-weight: bold;
  z-index: 200;
  transition: left 1s ease-out, top 1s ease-out;
}

.box {
  position: absolute;
  width: 50px;
  height: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: black;
  font-weight: bold;
  z-index: 200;
  transition: left 1s ease-out, top 1s ease-out;
}

.box:nth-child(1) {
  top: 25%;
  left: 25%;
  background-color: #c3a6ff;
}

.box:nth-child(2) {
  top: 25%;
  left: 50%;
  background-color: #fffba6;
}

.box:nth-child(3) {
  top: 25%;
  left: 75%;
  background-color: #ffa6a6;
}

.box:nth-child(4) {
  top: 75%;
  left: 25%;
  background-color: #ceffa6;
}

.box:nth-child(5) {
  top: 75%;
  left: 50%;
  background-color: #ffa6ed;
}

:deep(.box:nth-child(6)) {
  top: 75%;
  left: 75%;
  background-color: #a6ffef;
}
</style>
