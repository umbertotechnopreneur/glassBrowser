<!--
  
 Made with love by Umberto Giacobbi at UmbertoGiacobbi.biz

 For any info ping me at hello@umbertogiacobbi.biz

-->

<template>
  <v-container :style="backgroundStyle" fluid class=" d-flex justify-center align-center">
    <!-- This is our outer window, the background changes dynamically at each refresh-->
    <section class="browser thumb" ref="browserSection" @mousemove="handleMouseMove">
      <v-container v-show="showTools" class="adminBar">
        <div class="title">Admin area</div>
        <v-row>
          <v-col cols="12">
            <p>Hey some pro tip:</p>
            <ul class="ml-8">
              <li>Press <b>h</b> to hide/show the admin area</li>
              <li>Press <b>s</b> to enable/disable 3d manipulation</li>
              <li>Press <b>r</b> to reset the perspective</li>
              <li>Press <b>n or m</b> will decrease or increase the scaling by 0.01 <b>b</b> will reset to 1</li>
              <li>Refresh the browser window to change the backgound image of the page.</li>
              <li>Drop the image on the designed area or the 'browser document' to chane it.</li>
            </ul>
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field v-model="browserTitle" clearable hide-details label="Page title"></v-text-field>
          </v-col>
          <v-col cols="12" md="8" class="d-flex align-center">
            <v-text-field v-model="imageUrl" clearable hide-details label="Image url (local or whatever)"></v-text-field>
            <v-btn class="mx-4" @drop.prevent="onFileDrop" @dragover.prevent>drop the screenshot here</v-btn>
          </v-col>
          <v-col cols="12" class="d-flex align-center justify-center">
            <v-switch hide-details label="Switch 3D manipulation via mouse on and off"
              v-model="enable3DManipulation"></v-switch>
            <v-text-field hide-details label="Current scale" class="mx-4" v-model="actualScaling"></v-text-field>
            <v-slider hide-details v-model="actualScaling" max="1.5" min="0.5" step="0.01">
            </v-slider>
            <v-chip class="mx-4" v-if="enable3DManipulation">3D manipulation
              enabled</v-chip>
            <v-chip class="mx-4" v-if="!enable3DManipulation">3D manipulation
              NOT enabled</v-chip>

            <v-btn size="small" @click="resetPerspective">reset perspective</v-btn>
          </v-col>
        </v-row>

        <p class="text-caption"><b>Help wanted:</b> For <a href="https://aginti.it">aginti.it</a> (and other projects) we
          use this tool extensively. If you have time consider to add some features to it. Thanks for your contribution!
        </p>

        <p class="text-caption">For example what about a better 3d handling? <a
            href="https://polypane.app/css-3d-transform-examples">Here</a> you can get some inspiration.</p>
      </v-container>

      <!-- === Title bar === -->
      <section class="titleBar">
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

        <div class="title">{{ browserTitle }}</div>

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
        <img @drop.prevent="onFileDrop" @dragover.prevent id="screenShot" cover :src="imageUrl" class="theScreenShot"
          width="100%" height="100%" />
      </section>

      <!-- === End Document area === -->

    </section>
  </v-container>
</template>

<script setup>
import { ref, computed, watch } from 'vue';

// Add here your variables values
const browserTitle = ref('Default browser title');

const scaleTransform = ref('');
const rotationTransform = ref('');

const showTools = ref(true);
const hovered = ref(true);
const enable3DManipulation = ref(false);
const imageUrl = ref('../../images/yourScreenshot.jpg');
const actualScaling = ref(1);

watch(actualScaling, (newValue, oldValue) => {
  // This function will run when actualScaling changes
  console.log(`actualScaling changed from ${oldValue} to ${newValue}`);

  scaleTransform.value = 'scale(' + newValue + ')';

  applyTransformations();
});

function applyTransformations() {
  const thumb = document.getElementsByClassName('thumb')[0];

  thumb.style.transform = scaleTransform.value + ' ' + rotationTransform.value;
}

// Got inspiration from https://codepen.io/MarioDesigns/pen/NdygoP
const handleMouseMove = (event) => {
  if (!enable3DManipulation.value)
    return;

  // Your mousemove logic here
  console.log(`Mouse moved at ${event.clientX}, ${event.clientY}`);

  //set the hovered var to true
  hovered.value = true;

  const thumb = document.getElementsByClassName('thumb')[0];

  const classes = thumb.classList;

  // Log the classes
  for (let i = 0; i < classes.length; i++) {
    console.log(classes[i]);
  }

  //on hover if thumb has class idle removes it
  if (classes.contains('idle')) {
    classes.remove('idle');
  }

  // Define vars
  //gets the half point horizontally
  var hCenter = thumb.offsetWidth / 2;
  //gets the half point vertically
  var vCenter = thumb.offsetHeight / 2;
  //gets the x coord of the pointer
  var relativeX = (event.pageX - thumb.offsetLeft);
  //gets the y coords of the pointer
  var relativeY = (event.pageY - thumb.offsetTop);
  //calculates the x rotation
  var xRotation = (relativeY - vCenter) * 0.1;
  //calculates the y rotation
  var yRotation = (relativeX - hCenter) * 0.05;

  //Apply rotation to the element
  rotationTransform.value = 'rotateX(' + xRotation + 'deg) rotateY(' + yRotation + 'deg)';

  applyTransformations();
};

function resetPerspective() {
  const thumb = document.getElementsByClassName('thumb')[0];
  thumb.style.transform = 'rotatex(0deg) rotatey(0deg)';
}

const randomNumber = ref(Math.floor(Math.random() * 17) + 1);

const backgroundStyle = computed(() => ({
  backgroundImage: `url('./images/backgrounds/background${randomNumber.value}.jpg')`,
  backgroundSize: 'cover',
}));

function onFileDrop(e) {
  if (e.dataTransfer.files.length > 1) {
    alert('Please drop only one file at a time');
    return;
  } else if (e.dataTransfer.files.length === 0) {
    alert('Please drop a file');
    return;
  }

  const file = e.dataTransfer.files[0];

  let nameWithoutExtension = file.name.split('.').slice(0, -1).join('.');
  browserTitle.value = nameWithoutExtension;

  let reader = new FileReader();

  reader.onload = function (e) {
    let img = document.getElementById('screenShot');
    img.src = e.target.result;
  }

  reader.readAsDataURL(file);
}

import { onMounted } from 'vue';

onMounted(async () => {
  document.addEventListener('keyup', function (event) {
    if (event.key === 'h') {
      console.log('The "h" key was pressed up.');

      showTools.value = !showTools.value;
    }

    if (event.key === 's') {
      console.log('The "s" key was pressed up.');

      enable3DManipulation.value = !enable3DManipulation.value;
    }

    if (event.key === 'r') {
      console.log('The "r" key was pressed up.');

      enable3DManipulation.value = false;
      resetPerspective();
    }

    if (event.key === 'n') {
      console.log('The "n" key was pressed up.');

      actualScaling.value = actualScaling.value - 0.01;
    }

    if (event.key === 'm') {
      console.log('The "m" key was pressed up.');

      actualScaling.value = actualScaling.value + 0.01;
    }

    if (event.key === 'b') {
      console.log('The "b" key was pressed up.');

      actualScaling.value = 1;
    }

  })


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

/* === Browser 3d layout  === */

.thumb {
  transform-style: preserve-3d;
  transform-origin: center;
  transition: all 0.2s linear;
  transform: rotatex(0deg) rotatey(0deg);

  &.idle {
    &:after {
      transform: translatez(25px) translatey(0px);
      opacity: 1;
    }

    &:before {
      transform: translatez(25px) translatey(0px);
      opacity: 1;
    }
  }

  &:after {
    content: 'Hover Me';
    font-size: 12px;
    color: silver;
    position: absolute;
    top: -55px;
    left: 50%;
    width: 80px;
    margin-left: -40px;
    background-color: rgba(255, 255, 255, 0.4);
    text-align: center;
    padding: 5px 0;
    border-radius: 3px;
    transform: translatez(25px) translatey(20px);
    transition: all 0.4s ease-in-out;
    opacity: 0;
  }

  &:before {
    content: '';
    position: absolute;
    top: -32px;
    left: 50%;
    margin-left: -10px;
    width: 0;
    height: 0;
    border-style: solid;
    border-width: 8px 10px 0 10px;
    border-color: rgba(255, 255, 255, 0.4) transparent transparent transparent;
    transform: translatez(25px) translatey(20px);
    transition: all 0.4s ease-in-out;
    opacity: 0;
  }

  .backlight {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    width: 320px;
    height: 180px;
    background-color: rgba(255, 255, 255, 0.1);
    box-shadow: 0px 0px 100px 40px rgba(255, 255, 255, 0.2);
    transform: translateZ(-40px);
    z-index: 1;
  }

  .player {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    width: 320px;
    height: 180px;
    opacity: 1;
    border-radius: 5px;
    background-color: black;
    background-image: url('https://raw.githubusercontent.com/Mario-Duarte/CodePen/main/assets/alien-world.jpg');
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
    transform: translateZ(20px);
    z-index: 2;
  }

  .shine {
    position: absolute;
    top: 0;
    left: 0;
    width: 320px;
    height: 180px;
    border-radius: 5px;
    /*
    background-color: rgba(255,255,255,1);
		background: radial-gradient(ellipse at 50% 50%, rgba(255,255,255,0.6) 0%,rgba(51,51,51,0) 100%);
    */
    transform: translateZ(20px);
    overflow: hidden;
    pointer-events: none;
    z-index: 3;
  }
}

/* === End Browser 3d layout  === */

.title {
  font-size: 1.1rem;
  letter-spacing: 0.1rem;
  text-transform: uppercase;
  color: white;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 1);
}

.adminBar {
  justify-content: space-between;
  border-radius: 12px;
  position: relative;
  background-color: rgba(255, 255, 255, 0.2);
  border-top: 1px solid rgba(255, 255, 255, 0.6);
  border-left: 1px solid rgba(255, 255, 255, 0.6);
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  border-right: 1px solid rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(32px);
}

.titleBar {
  width: 100;
  padding: 4px;
  margin: 4px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.documentArea {
  border-radius: 12px;
  position: relative;
  border-top: 1px solid rgba(255, 255, 255, 0.6);
  border-left: 1px solid rgba(255, 255, 255, 0.6);
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  border-right: 1px solid rgba(0, 0, 0, 0.1);

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
  border-radius: 16px;
  padding: 10px;
  letter-spacing: 1px;
  text-decoration: none;
  overflow: hidden;
  color: #fff;
  font-weight: 400px;
  z-index: 1;
  transition: 0.5s;
  backdrop-filter: blur(15px);

  border-top: 1px solid rgba(255, 255, 255, 0.6);
  border-left: 1px solid rgba(255, 255, 255, 0.6);
  border-bottom: 1px solid rgba(0, 0, 0, 0.3);
  border-right: 1px solid rgba(0, 0, 0, 0.3);
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
  background: #12c12f;
  box-shadow: 0 0 5px #12c12f, 0 0 15px #12c12f, 0 0 30px #12c12f,
    0 0 60px #12c12f;
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