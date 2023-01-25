<template>
  <main id="main">

    <NetworkInteractionComponent ref="childComponentRef">
      <ComponentTest class="box" id="box1"></ComponentTest>
      <ComponentTest class="box" id="box2"></ComponentTest>
      <ComponentTest class="box" id="box3"></ComponentTest>
      <ComponentTest class="box" id="box4"></ComponentTest>
      <ComponentTest class="box" id="box5"></ComponentTest>
      <ComponentTest class="box" id="box6"></ComponentTest>
    </NetworkInteractionComponent>
    <button @click="animate()">Start animation</button>
  </main>
</template>

<script>
import NetworkInteractionComponent from "@/components/NetworkInteractionComponent";
import ComponentTest from "@/components/ComponentTest";

export default {
  name: 'App',
  mounted() {
    this.$refs.childComponentRef.setPackage("box1", "package1")
    this.$refs.childComponentRef.setPackage("box2", "package2")
    this.$refs.childComponentRef.setPackage("box3", "package3")
    this.$refs.childComponentRef.setPackage("box4", "package4")
    this.$refs.childComponentRef.drawLine("box1", "box6")
    this.$refs.childComponentRef.drawLine("box3", "box4")
    this.$refs.childComponentRef.drawLine("box2", "box5")

  },
  methods: {
    animate(){
      this.$refs.childComponentRef.animatePackage("box6", "package1")
      this.$refs.childComponentRef.animatePackage("box4", "package3")
      this.$refs.childComponentRef.animatePackage("box3", "package4")
      this.$refs.childComponentRef.animatePackage("box5", "package2")
    }
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
  display: flex;
  width: max-content;
  justify-content: center;
  align-items: center;
  color: black;
  font-weight: bold;
  z-index: 50;
  transition: left 1s ease-out, top 1s ease-out;
}

.box:nth-child(1) {
  top: 5%;
  left: 5%;
  background-color: #c3a6ff;
}

.box:nth-child(2) {
  top: 8%;
  left: 30%;
  background-color: #fffba6;
}

.box:nth-child(3) {
  top: 12%;
  left: 75%;
  background-color: #ffa6a6;
}

.box:nth-child(4) {
  top: 75%;
  left: 10%;
  background-color: #ceffa6;
}

.box:nth-child(5) {
  top: 75%;
  left: 45%;
  background-color: #ffa6ed;
}

:deep(.box:nth-child(6)) {
  top: 75%;
  left: 77%;
  background-color: #a6ffef;
}
</style>
