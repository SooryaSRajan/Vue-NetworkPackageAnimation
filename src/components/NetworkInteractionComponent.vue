<template>
  <!--
      Note:
      :deep(.box:nth-child(6))
      Use deep in parent CSS to restrict the scope of the CSS selector to the child component.

      Methods packaged with the module:
      setPackage(element on which package should rest, id for the package)
      animatePackage(target element, package id of the package to animate)
      drawLine(source element id, target element id)
  -->
  <div id="margin-container">
    <div id="root">
      <svg id="lineCanvas">
        <!--This is where the lines for the packages go-->
      </svg>
      <div id="overlay">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "NetworkInteractionComponent",
  data() {
    return {
      elementMap: {}
    }
  },
  mounted() {
    let marginContainer = document.getElementById("margin-container").getBoundingClientRect();

    let width = (marginContainer.width - 50) + "px";
    let height = (marginContainer.height - 50) + "px";

    document.getElementById("root").style.width = width
    document.getElementById("root").style.height = height
    document.getElementById("lineCanvas").style.width = width
    document.getElementById("lineCanvas").style.height = height
    document.getElementById("overlay").style.width = width
    document.getElementById("overlay").style.height = height
  },
  methods: {
    drawSVGLine(x1, y1, x2, y2) {
      let svg = document.getElementById('lineCanvas');
      let line = document.createElementNS("http://www.w3.org/2000/svg", "line");
      line.setAttribute("x1", x1);
      line.setAttribute("y1", y1);
      line.setAttribute("x2", x2);
      line.setAttribute("y2", y2);
      line.setAttribute("style", "stroke:rgb(0,0,0);stroke-width:1");
      svg.appendChild(line);
    },
    animatePackage(target, packageID) {
      let element = document.getElementById(target);
      let packageDOM = document.getElementById(packageID);

      let currentPackageID = this.elementMap[packageID];
      let currentElement = document.getElementById(currentPackageID);

      //setting element to center of current element
      let x1T = currentElement.offsetLeft + (currentElement.offsetWidth / 2) - (packageDOM.offsetWidth / 2);
      let y1T = currentElement.offsetTop + (currentElement.offsetHeight / 2) - (packageDOM.offsetHeight / 2);

      packageDOM.style.left = x1T + 'px';
      packageDOM.style.top = y1T + 'px';

      //wait for 3 seconds
      setTimeout(() => {
        //setting element to center of target element
        let x1E = element.offsetLeft + (element.offsetWidth / 2) - (packageDOM.offsetWidth / 2);
        let y1E = element.offsetTop + (element.offsetHeight / 2) - (packageDOM.offsetHeight / 2);

        packageDOM.style.left = x1E + 'px';
        packageDOM.style.top = y1E + 'px';

        setTimeout(() => {
          //setting element to center of target element
          let x1E = element.offsetLeft + (element.offsetWidth) - 10;
          let y1E = element.offsetTop + (element.offsetHeight) - 10;

          packageDOM.style.left = x1E + 'px';
          packageDOM.style.top = y1E + 'px';
        }, 2000);

      }, 2000);
    },
    drawLine(id1, id2) {
      let elementA = document.getElementById(id1);
      let elementB = document.getElementById(id2);

      let x1 = elementA.offsetLeft + (elementA.offsetWidth / 2);
      let y1 = elementA.offsetTop + (elementA.offsetHeight / 2);
      let x2 = elementB.offsetLeft + (elementB.offsetWidth / 2);
      let y2 = elementB.offsetTop + (elementB.offsetHeight / 2);

      this.drawSVGLine(x1, y1, x2, y2);
    },
    setPackage(id, packageID) {
      let elements = document.getElementById(id);
      let target = document.getElementById('overlay');

      this.elementMap[packageID] = id;

      let xT = elements.offsetLeft + (elements.offsetWidth) - 10;
      let yT = elements.offsetTop + (elements.offsetHeight) - 10;

      let newDiv = document.createElement('div');
      newDiv.id = packageID;
      newDiv.innerText = "Package";

      //set position of new div
      //TODO: Change package CSS

      newDiv.style.left = xT.toString() + "px";
      newDiv.style.top = yT.toString() + "px";
      newDiv.style.backgroundColor = "yellow";
      newDiv.style.color = "black"
      newDiv.style.width = "min-content";
      newDiv.style.padding = "10px";
      newDiv.style.borderRadius = "10px";
      newDiv.style.position = 'absolute';
      newDiv.style.fontSize = "10px";
      newDiv.style.transition = "left 1s ease-out, top 1s ease-out";
      newDiv.style.zIndex = "100";

      console.log(newDiv.style.left, newDiv.style.top, "new div")

      target.appendChild(newDiv);
    },
  }
}
</script>

<style scoped>
#margin-container {
  width: 100%;
  height: 100%;
  box-sizing: border-box;
  padding: 25px;
  overflow: scroll;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: left 1s ease-out, top 1s ease-out;
}

#root {
  border-radius: 10px;
  background-color: #F9FAFE;
  box-shadow: 2px 3px 10px 2px #D7DFFF;
  text-align: center;
  position: relative;
  overflow: scroll;
}

#lineCanvas {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 0;
}

#overlay {
  position: relative;
}
</style>