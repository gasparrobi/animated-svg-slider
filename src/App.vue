<template>
  <div id="app">
    <Slider/>
    <span>
      inspired by:
      <a
        href="https://dribbble.com/shots/3845034-Listening-now-Kishi-Bashi"
        target="_blank"
        rel="noreferrer noopener"
      >Stan Yakusevich</a>
      <img
        src="https://cdn.dribbble.com/assets/dribbble-ball-icon-e94956d5f010d19607348176b0ae90def55d61871a43cb4bcb6d771d8d235471.svg"
        alt="dribbble logo"
      >
    </span>
    
    <span>
      <a href="https://github.com/gasparrobi/animated-svg-slider" target="_blank" rel="noreferrer noopener">check out the code on github</a>
      <div class="github-logo"></div>
    </span>
  </div>
</template>

<script>
import Slider from "./components/Slider";

export default {
  name: "App",
  components: {
    Slider
  }
};
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  background: #dde7f3;
  margin: 0 auto;
  font-family: "Montserrat", sans-serif;
  background-color: #dde7f3;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 60px 10px;
}

span {
  margin-top: 30px;
  text-transform: uppercase;
  font-size: 9px;
  font-weight: 600;
  color: rgba(57, 117, 167, 0.445);
  display: flex;
  justify-content: center;
  align-items: center;
}

a {
  font-weight: 800;
  /* text-decoration: none; */
  color: rgba(57, 117, 167, 0.445);
  margin: 0 5px;
}

img {
  width: 12px;
}

.github-logo {
  width: 12px;
  height: 12px;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' height='128' width='128' class='octicon octicon-mark-github' viewBox='0 0 16 16' version='1.1' aria-hidden='true'%3E%3Cpath fill-rule='evenodd' d='M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z'%3E%3C/path%3E%3C/svg%3E");
  background-size: contain;
}
</style>
