<template>
  <main id="main">

    <NetworkInteractionComponent ref="childComponentRef" :on-package-animation-end="onAnimationEnd">
      <EndSystemComponent class="box" id="box1" package-id="package1" top="10%" left="10%"
                          :data="['SYN SYN SYN SYN', 'ACK (ack data)', input]" package-background-color="#8ef6ff">
        <h1>
          Hey there
        </h1>
      </EndSystemComponent>
      <EndSystemComponent class="box" id="box2" package-id="package2" top="10%" left="45%"
                          :data="['SYN SYN SYN SYN', 'ACK (ack data)', input, input]" package-background-color="#ae8eff">
        <h1>
          Hey there
        </h1>
      </EndSystemComponent>
      <EndSystemComponent class="box" id="box3" top="10%" left="80%" package-id="package3" :data="['SYN SYN SYN SYN', 'ACK (ack data)', input, input, input]">
        <h1>
          Hey there
        </h1>
      </EndSystemComponent>
      <EndSystemComponent class="box" id="box4" top="80%" left="10%" package-id="package4" :data="['SYN SYN SYN SYN', 'ACK (ack data)', input, input, input]">
        <h1>
          Hey there
        </h1>
      </EndSystemComponent>
      <EndSystemComponent class="box" id="box5" top="80%" left="45%" package-id="package5" :data="['SYN SYN SYN SYN', 'ACK (ack data)', input, input, input]">
        <h1>
          Hey there
        </h1>
      </EndSystemComponent>
      <EndSystemComponent class="box" id="box6" top="80%" left="80%" package-id="package6" :data="['SYN SYN SYN SYN', 'ACK (ack data)', input, input, input]">
        <h1>
          Hey there
        </h1>
      </EndSystemComponent>
    </NetworkInteractionComponent>
    <button @click="animate()">Start animation</button>
    <button @click="animateBack()">Start animation</button>
    <PackageComponent :data="[]"></PackageComponent>
    <input v-model="input">
  </main>
</template>

<script>
import NetworkInteractionComponent from "@/components/network-components/NetworkInteractionComponent";
import EndSystemComponent from "@/components/network-components/EndSystemComponent";
import PackageComponent from "@/components/network-components/PackageComponent";

export default {
  name: 'App',
  mounted() {
    this.$refs.childComponentRef.drawLine("box1", "box6")
    this.$refs.childComponentRef.drawLine("box3", "box4")
    this.$refs.childComponentRef.drawLine("box2", "box5")
  },
  methods: {
    animate() {
      this.$refs.childComponentRef.animatePackage("box5", "package1", "box1")
      this.$refs.childComponentRef.animatePackage("box5", "package2", "box2")
      this.$refs.childComponentRef.animatePackage("box5", "package3", "box3")
      this.$refs.childComponentRef.animatePackage("box2", "package4", "box4")
      this.$refs.childComponentRef.animatePackage("box2", "package5", "box5")
      this.$refs.childComponentRef.animatePackage("box2", "package6", "box6")
    },
    animateBack() {
      this.$refs.childComponentRef.animatePackage("box1", "package1", "box5", () => {})
      this.$refs.childComponentRef.animatePackage("box2", "package2", "box5")
      this.$refs.childComponentRef.animatePackage("box3", "package3", "box5")
      this.$refs.childComponentRef.animatePackage("box4", "package4", "box2")
      this.$refs.childComponentRef.animatePackage("box5", "package5", "box2")
      this.$refs.childComponentRef.animatePackage("box6", "package6", "box2")
    },
    onAnimationEnd(id) {
      console.log("Animation ended for id: " + id)
      if (id === "package1") {
        this.packageOneReached = true;
      } else if (id === "package2") {
        this.packageTwoReached = true;
      }

      if (this.packageOneReached && this.packageTwoReached) {
        console.log("Both packages reached their destination")

      }
      this.$refs.childComponentRef.arrangePackages("box5")
      this.$refs.childComponentRef.arrangePackages("box2")
    }
  },
  data() {
    return {
      input: "test",
      packageOneReached: false,
      packageTwoReached: false,
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

