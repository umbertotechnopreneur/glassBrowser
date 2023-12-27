<!--
  
 Made with love by Umberto Giacobbi at UmbertoGiacobbi.biz

 For any info ping me at hello@umbertogiacobbi.biz

-->

<template>
  <v-container :style="backgroundStyle" fluid class=" d-flex justify-center align-center">
    <!-- This is our outer window, the background changes dynamically at each refresh-->
    <section class="browser">
      <!-- === Title bar === -->
      <section class="titleBar d-flex justify-start align-center">
        <!-- Would be nice if this works by darkening the background? -->
        <button id="toggler" class="darkLightThemeTogglerbutton">
          <svg id="dark" xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" fill="black" viewBox="0 0 16 16"
            style="display: none;">
            <path
              d="M6 .278a.768.768 0 0 1 .08.858 7.208 7.208 0 0 0-.878 3.46c0 4.021 3.278 7.277 7.318 7.277.527 0 1.04-.055 1.533-.16a.787.787 0 0 1 .81.316.733.733 0 0 1-.031.893A8.349 8.349 0 0 1 8.344 16C3.734 16 0 12.286 0 7.71 0 4.266 2.114 1.312 5.124.06A.752.752 0 0 1 6 .278z" />
            <path
              d="M10.794 3.148a.217.217 0 0 1 .412 0l.387 1.162c.173.518.579.924 1.097 1.097l1.162.387a.217.217 0 0 1 0 .412l-1.162.387a1.734 1.734 0 0 0-1.097 1.097l-.387 1.162a.217.217 0 0 1-.412 0l-.387-1.162A1.734 1.734 0 0 0 9.31 6.593l-1.162-.387a.217.217 0 0 1 0-.412l1.162-.387a1.734 1.734 0 0 0 1.097-1.097l.387-1.162zM13.863.099a.145.145 0 0 1 .274 0l.258.774c.115.346.386.617.732.732l.774.258a.145.145 0 0 1 0 .274l-.774.258a1.156 1.156 0 0 0-.732.732l-.258.774a.145.145 0 0 1-.274 0l-.258-.774a1.156 1.156 0 0 0-.732-.732l-.774-.258a.145.145 0 0 1 0-.274l.774-.258c.346-.115.617-.386.732-.732L13.863.1z" />
          </svg>
          <svg id="light" xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" fill="currentColor"
            viewBox="0 0 16 16" style="display: block;">
            <path
              d="M8 12a4 4 0 1 0 0-8 4 4 0 0 0 0 8zM8 0a.5.5 0 0 1 .5.5v2a.5.5 0 0 1-1 0v-2A.5.5 0 0 1 8 0zm0 13a.5.5 0 0 1 .5.5v2a.5.5 0 0 1-1 0v-2A.5.5 0 0 1 8 13zm8-5a.5.5 0 0 1-.5.5h-2a.5.5 0 0 1 0-1h2a.5.5 0 0 1 .5.5zM3 8a.5.5 0 0 1-.5.5h-2a.5.5 0 0 1 0-1h2A.5.5 0 0 1 3 8zm10.657-5.657a.5.5 0 0 1 0 .707l-1.414 1.415a.5.5 0 1 1-.707-.708l1.414-1.414a.5.5 0 0 1 .707 0zm-9.193 9.193a.5.5 0 0 1 0 .707L3.05 13.657a.5.5 0 0 1-.707-.707l1.414-1.414a.5.5 0 0 1 .707 0zm9.193 2.121a.5.5 0 0 1-.707 0l-1.414-1.414a.5.5 0 0 1 .707-.707l1.414 1.414a.5.5 0 0 1 0 .707zM4.464 4.465a.5.5 0 0 1-.707 0L2.343 3.05a.5.5 0 1 1 .707-.707l1.414 1.414a.5.5 0 0 1 0 .708z" />
          </svg>
        </button>

        <div>{{ browserTitle }}</div>

        <!-- Here we put the window actions -->
        <div class="actionButtons d-flex justify-end align-center">
          <div class="titleBarActionButtonsContainer">
            <div class="button"><a href="#"><v-icon>mdi-window-maximize</v-icon></a></div>
            <div class="button"><a href="#"><v-icon>mdi-window-minimize</v-icon></a></div>
            <div class="button"><a href="#"><v-icon>mdi-close</v-icon></a></div>
          </div>
        </div>
      </section>

      <!-- === End Title bar === -->

      <!-- === Document area === -->

      <section class="documentArea">
        <v-img cover src="../../images/yourScreenshot.jpg" class="theScreenShot" width="100%" height="100%"></v-img>
      </section>

      <!-- === End Document area === -->

    </section>
  </v-container>
</template>

<script setup>
import { ref, computed, nextTick } from 'vue';

// Add here your variables values
const browserTitle = computed(() => 'Aginti - The gallery');

const randomNumber = ref(Math.floor(Math.random() * 8) + 1);

const backgroundStyle = computed(() => ({
  backgroundImage: `url('./images/backgrounds/gallery${randomNumber.value}.jpg')`,
  backgroundSize: 'cover',
}));

import { onMounted } from 'vue';

onMounted(async () => {
  try {
    const VanillaTilt = await import('vanilla-tilt');

    nextTick(() => {
      VanillaTilt.init(document.querySelector('.browser'), {
        max: 15,
        speed: 1000,
        glare: true,
        scale: 1.1,
        gyroscope: true,
        "max-glare": 0.5,
      });
    });

  } catch (error) {
    throw ('Error loading VanillaTilt', error);
  }
});
</script>

<style scoped>
/* === Browser overall layout  === */

.browser {
  background-image: linear-gradient(to bottom right,
      rgba(255, 255, 255, 0.3) 0%,
      rgba(255, 255, 255, 0.1) 100%);
  backdrop-filter: blur(6px);
  border-radius: 12px;
  width: 80%;
  height: 80%;
  border-top: 1px solid rgba(255, 255, 255, 0.5);
  border-left: 1px solid rgba(255, 255, 255, 0.5);
  padding-top: 4px;
  padding-left: 4px;
  padding-right: 4px;
  padding-bottom: 4px;
  box-shadow: rgba(255, 255, 255, 0.5) -20px -20px 45px inset,
    rgba(0, 0, 0, 0.1) 10px 10px 20px, rgba(0, 0, 0, 0.06) 5px 5px 10px;
  position: relative;

  &::before {
    content: "";
    display: block;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-image: linear-gradient(135deg,
        rgba(255, 255, 255, 0) 0%,
        rgba(255, 255, 255, 0.05) 40%,
        rgba(255, 255, 255, 0) 40%);
    pointer-events: none;
  }
}

.titleBar {
  width: 100;
  padding: 4px;
  margin: 4px;
}

.titleBar .actionButtons {
  /* Nothing for now */
} 

.documentArea {
  border-radius: 12px;
  position: relative;
  border-top: 1px solid rgba(50, 50, 50, 0.5);
  border-left: 1px solid rgba(50, 50, 50, 0.5);
  border-bottom: 1px solid rgba(50, 50, 50, 0.5);
  border-right: 1px solid rgba(50, 50, 50, 0.5);
  background-color: white;
}

.theScreenShot {
  border-radius: 12px;

  /* Cast a light reflection */
  &::before {
    content: "";
    display: block;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-image: linear-gradient(135deg,
        rgba(255, 255, 255, 0) 0%,
        rgba(255, 255, 255, 0.05) 40%,
        rgba(255, 255, 255, 0) 40%);
    pointer-events: none;
  }
}

/* === End Browser overall layout  === */

.darkLightThemeTogglerbutton {
  position: relative;
  top: -4px;
  left: -4px;
  font-size: 13px;
  padding: 8px 12px;
  background-color: var(--button-bg);
  border-top-left-radius: 12px;
  border-bottom-right-radius: 12px;
  color: #fff;
  cursor: pointer;
  border: none;
  outline: none;
  will-change: auto;
  backdrop-filter: blur(4px);
  transition: all .1s ease-in-out;
  z-index: 5;

  &:hover,
  &:focus {
    box-shadow: 0px 10px 25px rgba(4, 37, 100, 0.12);
    border: 1px solid rgba(#fff, .2);
    background-color: var(--button-bg-hover);
    border-color: rgba(#fff, .08);
    transform: scale(1.25);
  }
}

/* Inspired by https://codepen.io/katarzynamarta/pen/rNdbbVq but revised by Umberto Giacobbi */

.titleBarActionButtonsContainer {
  width: Auto;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.titleBarActionButtonsContainer .button {
  position: relative;
  top: 0;
  left: 0;
  margin: 2px;
  width: 50px;
  height: 25px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.titleBarActionButtonsContainer .button a {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgba(255, 255, 255, 0.05);
  box-shadow: 0 15px 15px rgba(0, 0, 0, 0.3);
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 30px;
  padding: 10px;
  letter-spacing: 1px;
  text-decoration: none;
  overflow: hidden;
  color: #fff;
  font-weight: 400px;
  z-index: 1;
  transition: 0.5s;
  backdrop-filter: blur(15px);
}

.titleBarActionButtonsContainer .button:hover a {
  letter-spacing: 3px;
}

.titleBarActionButtonsContainer .button a::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 50%;
  height: 100%;
  background: linear-gradient(to left, rgba(255, 255, 255, 0.15), transparent);
  transform: skewX(45deg) translate(0);
  transition: 0.5s;
  filter: blur(0px);
}

.titleBarActionButtonsContainer .button:hover a::before {
  transform: skewX(45deg) translate(200px);
}

.titleBarActionButtonsContainer .button::before {
  content: "";
  position: absolute;
  left: 50%;
  transform: translatex(-50%) translateY(-50%);
  bottom: -5px;
  width: 30px;
  height: 10px;
  background: #f00;
  border-radius: 10px;
  transition: 0.5s;
  transition-delay: 0.5;
}

/* Lightup button */
.titleBarActionButtonsContainer .button:hover::before {
  bottom: 0;
  height: 50%;
  width: 80%;
  border-radius: 30px;
}

.titleBarActionButtonsContainer .button::after {
  content: "";
  position: absolute;
  left: 50%;
  transform: translatex(-50%);
  top: -5px;
  width: 30px;
  /* height: 10px; */
  background: #f00;
  border-radius: 10px;
  transition: 0.5s;
  transition-delay: 0.5;
}

/* Lightup button*/
.titleBarActionButtonsContainer .button:hover::after {
  top: 0;
  height: 50%;
  width: 80%;
  border-radius: 30px;
}

/* Change 1*/
.titleBarActionButtonsContainer .button:nth-child(1)::before,
.titleBarActionButtonsContainer .button:nth-child(1)::after {
  background: #1eff45;
  box-shadow: 0 0 5px #1eff45, 0 0 15px #1eff45, 0 0 30px #1eff45,
    0 0 60px #1eff45;
}

/* 2 */
.titleBarActionButtonsContainer .button:nth-child(2)::before,
.titleBarActionButtonsContainer .button:nth-child(2)::after {
  background: #2db2ff;
  box-shadow: 0 0 5px #2db2ff, 0 0 15px #2db2ff, 0 0 30px #2db2ff,
    0 0 60px #2db2ff;
}

/* 3 */
.titleBarActionButtonsContainer .button:nth-child(3)::before,
.titleBarActionButtonsContainer .button:nth-child(3)::after {
  background: #ff1f71;
  box-shadow: 0 0 5px #ff1f71, 0 0 15px #ff1f71, 0 0 30px #ff1f71,
    0 0 60px #ff1f71;
}
</style>