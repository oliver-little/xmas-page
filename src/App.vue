<script setup lang="ts">
import gsap from "gsap";
import { ref } from "vue";

const count = ref(1);

const startNext = () => {
  const selector = `.circle:nth-of-type(${count.value})`;
  if (count.value >= 10) {
    gsap
      .timeline()
      .to(selector, {
        width: "100vw",
        height: "100vh",
        duration: 0.5,
      })
      .to(
        selector,
        {
          borderRadius: "0",
          ease: "power1.out",
          duration: 0.5,
        },
        "<"
      )
      .to(
        selector,
        {
          backgroundColor: "#6baaf2",
          duration: 2.5
        },
        "<"
      )
      .to(
        ".albumArt",
        {
          opacity: 1,
          duration: 5,
        },
        "+=1"
      )

      .to(
        ".albumArt",
        {
          filter: "blur(0px)",
          ease: "power1.in",
          duration: 2.5,
        },
        "-=2.5"
      )
      .to("h1", {
        opacity: 1,
        duration: 1
      }, "+=2")
      .play();
    return;
  }

  gsap
    .timeline()
    .to(selector, {
      scale: count.value * 1.5,
      opacity: 0,
      ease: "power1.out",
      duration: 1,
    })
    .play();

  count.value++;
};
</script>

<template>
  <div class="clickable" @click="startNext"></div>
  <img class="albumArt" src="/poster.jpg" />
  <div class="text">
    <h1>Friday 5th June 2026</h1>
  </div>
  <div class="circleContainer">
    <div class="circle"></div>
    <div class="circle"></div>
    <div class="circle"></div>
    <div class="circle"></div>
    <div class="circle"></div>
    <div class="circle"></div>
    <div class="circle"></div>
    <div class="circle"></div>
    <div class="circle"></div>
    <div class="circle"></div>
  </div>
</template>

<style>
body {
  background-color: #222;
}

#app {
  overflow: hidden;
}

.albumArt {
  opacity: 0;
  width: 90vw;
  border-radius: 10px;
  position: absolute;
  top: 50%;
  left: 50%;
  translate: -50% -70%;
  z-index: 1;
  filter: blur(20px);
}

.text {
  position: absolute;
  bottom: 10%;
  left: 0%;
  width: 100vw;
  z-index: 1;
  display: flex;
  align-items: stretch;

  h1 {
    flex: 1;
    text-align: center;
    opacity: 0;
    color: #fff;
    font-size: 2.5rem;
    border-radius: 10px;
    font-family: "Dancing Script", cursive;
    font-optical-sizing: auto;
    font-weight: 500;
    font-style: normal;
  }
}


.clickable {
  z-index: 10;
  position: absolute;
  top: -3000px;
  left: -3000px;
  width: 6000px;
  height: 10000px;
}

.circleContainer {
  position: absolute;
  top: 50%;
  left: 50%;
}

.circle {
  background-color: #eee;
  border-radius: 100%;
  width: 4rem;
  height: 4rem;
  position: absolute;
  translate: -50% -50%;
}
</style>
