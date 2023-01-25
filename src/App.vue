<template>
  <main id="main">

    <NetworkInteractionComponent ref="childComponentRef">
      <EndSystemComponent class="box" id="box1" package-id="package1" top="10%" left="10%"
                          :data="['SYN SYN SYN SYN', 'ACK (ack data)', input]">
        <h1>
          Hey there
        </h1>
      </EndSystemComponent>
      <EndSystemComponent class="box" id="box2" package-id="package2" top="10%" left="45%"
                          :data="['SYN SYN SYN SYN', 'ACK (ack data)']">
        <h1>
          Hey there
        </h1>
      </EndSystemComponent>
      <EndSystemComponent class="box" id="box3" top="10%" left="80%">
        <h1>
          Hey there
        </h1>
      </EndSystemComponent>
      <EndSystemComponent class="box" id="box4" top="80%" left="10%">
        <h1>
          Hey there
        </h1>
      </EndSystemComponent>
      <EndSystemComponent class="box" id="box5" top="80%" left="45%">
        <h1>
          Hey there
        </h1>
      </EndSystemComponent>
      <EndSystemComponent class="box" id="box6" top="80%" left="80%">
        <h1>
          Hey there
        </h1>
      </EndSystemComponent>
    </NetworkInteractionComponent>
    <button @click="animate()">Start animation</button>
    <PackageComponent :data="data"></PackageComponent>
    <input v-model="input">
  </main>
</template>

<script>
import NetworkInteractionComponent from "@/components/NetworkInteractionComponent";
import EndSystemComponent from "@/components/EndSystemComponent";
import PackageComponent from "@/components/PackageComponent";

export default {
  name: 'App',
  mounted() {
    this.$refs.childComponentRef.drawLine("box1", "box6")
    this.$refs.childComponentRef.drawLine("box3", "box4")
    this.$refs.childComponentRef.drawLine("box2", "box5")

  },
  methods: {
    animate() {
      this.$refs.childComponentRef.animatePackageNew("box6", "package1", "box1")
      this.$refs.childComponentRef.animatePackageNew("box5", "package2", "box2")
    }
  },
  data() {
    return {
      input: "test"

    }
  },
  components: {PackageComponent, EndSystemComponent, NetworkInteractionComponent},
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

div {
  transition: ease-in-out 1s;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 0;
  padding: 0;
  transition: ease-in-out 1s;
}
</style>

