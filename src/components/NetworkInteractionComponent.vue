
<template>
<!--
    Note:
    :deep(.box:nth-child(6))
    Use deep in parent CSS to restrict the scope of the CSS selector to the child component.
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
    return {}
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
    animatePackage(target) {
      //TODO: Make target orientation dynamic
      if (target < 0 || target > 5) {
        return;
      }

      let element = document.getElementById(target);
      let packageDOM = document.getElementById('package');

      let xT = element.offsetLeft + 50;
      let yT = element.offsetTop + 50;

      let xE = packageDOM.offsetLeft;
      let yE = packageDOM.offsetTop;

      packageDOM.style.left = xE + 'px';
      packageDOM.style.top = yE + 'px';

      packageDOM.style.left = xT + 'px';
      packageDOM.style.top = yT + 'px';

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
    setPackage(id, position) {
      let elements = document.getElementById(id);
      let target = document.getElementById('overlay');

      //TODO: get the coordinates of the element and the size and place package in left, top, right, bottom as needed

      let xT = elements.offsetLeft
      let yT = elements.offsetTop

      //TODO: Change math behind logic, does not work right

      if (position === "TL") {
        //top left of the element target, get target dimensions, TL - top left, so + 1/2 of height of element and - 1/2 of width of element
        xT = xT - (elements.offsetWidth / 2)
        yT = yT - (elements.offsetHeight / 2)
      } else if (position === "TR") {
        //top right of the element target, get target dimensions, TR - top right, so + 1/2 of height of element and + 1/2 of width of element
        xT = xT + (elements.offsetWidth / 2)
        yT = yT - (elements.offsetHeight / 2)
      } else if (position === "BL") {
        //bottom left of the element target, get target dimensions, BL - bottom left, so - 1/2 of height of element and - 1/2 of width of element
        xT = xT - (elements.offsetWidth / 2)
        yT = yT + (elements.offsetHeight / 2)
      } else if (position === "BR") {
        //bottom right of the element target, get target dimensions, BR - bottom right, so - 1/2 of height of element and + 1/2 of width of element
        xT = xT + (elements.offsetWidth / 2)
        yT = yT + (elements.offsetHeight / 2)
      } else if (position === "T") {
        //top of the element target, get target dimensions, T - top, so + 1/2 of height of element
        yT = yT - (elements.offsetHeight / 2)
      } else if (position === "B") {
        //bottom of the element target, get target dimensions, B - bottom, so - 1/2 of height of element
        yT = yT + (elements.offsetHeight / 2)
      } else if (position === "L") {
        //left of the element target, get target dimensions, L - left, so - 1/2 of width of element
        xT = xT - (elements.offsetWidth / 2)
      } else if (position === "R") {
        //right of the element target, get target dimensions, R - right, so + 1/2 of width of element
        xT = xT + (elements.offsetWidth / 2)
      }

      console.log(xT, yT, "coords")

      //create new div
      let newDiv = document.createElement('div');
      //TODO: Make package ID dynamic
      newDiv.id = 'package';
      newDiv.innerText = "Package";

      //set position of new div

      //TODO: Change package CSS

      newDiv.style.left = xT + 'px';
      newDiv.style.top = yT + 'px';
      newDiv.style.backgroundColor = "yellow";
      newDiv.style.color = "black"
      newDiv.style.width = "min-content";
      newDiv.style.padding = "10px";
      newDiv.style.borderRadius = "10px";
      newDiv.style.position = 'relative';
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