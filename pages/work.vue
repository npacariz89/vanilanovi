<template>
  <div>
    <div class="container">
      <div class="flex-row-container">
        <div class="vf-header">
          <h1>Logo</h1>
          <ul class="vf-header-navigation">
            <nuxt-link class="vf-header-item" to="/work">Work</nuxt-link>/
            <nuxt-link class="vf-header-item" to="/about_us">About us</nuxt-link>
          </ul>
        </div>
        <div class="flex-row-item" v-for="(video, index) in LIST_OF_VIDEOS" :key="video.id">
          <p>{{index}} / {{video.title}} / {{video.clientName}}</p>
          <img class="vf-work-main-card-image" :src="video.thumbnail">
        </div>
        <svg viewBox="0 0 350 350" preserveAspectRatio="xMinYMin meet">
          <path
            d="M0.00,49.98 C149.99,150.00 349.20,-49.98 500.00,49.98 L500.00,150.00 L0.00,150.00 Z"
            style="stroke: none; fill: orange;"
          ></path>
        </svg>
      </div>
    </div>
  </div>
</template>

<script>
import { LIST_OF_VIDEOS, HOME_PAGE_VIDEOS } from "../core/constants";
export default {
  data() {
    return {
      LIST_OF_VIDEOS
    };
  }
};
</script>
<style>
.vf-work-main-grid {
  background: black;
  display: flex;
  flex-wrap: wrap;
}
.vf-work-main-card {
  background: red;
  flex-grow: 33.33%;
  max-width: 33%;
  z-index: 1;
}
.vf-work-main-card-image {
  width: 300px;
  z-index: 1;
}

.flex-row-container {
  flex-grow: 1;
  flex-basis: 0;
  display: flex;
  flex-wrap: wrap;
  margin-right: -1.5rem;
  margin-left: 3rem;
  padding-top: 5rem;
}
.flex-row-container > .flex-row-item {
  flex: 1 1 30%;
}
svg {
  display: inline-block;
  position: absolute;
  top: 0;
  left: 0;
  margin-top: 400px;
}
.container {
  background-color: black; /* Old browsers */
  background-image: -webkit-gradient(
    linear,
    left top,
    left bottom,
    color-stop(50%, black),
    color-stop(50%, black),
    color-stop(50%, orange)
  );
  background-image: -webkit-linear-gradient(
    top,
    black 50%,
    black 50%,
    orange 50%
  );
  background-image: -moz-linear-gradient(top, black 50%, black 50%, orange 50%);
  background-image: linear-gradient(black 50%, black 50%, orange 50%);
  display: inline-block;
  position: relative;
  width: 100%;
  padding-bottom: 100%;
  vertical-align: middle;
  overflow: hidden;
}

.vf-header {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  top: 0;
  width: 100%;
  background: transparent;
  color: white;
  line-height: 0.5rem;
  padding: 2.4rem;
  overflow: hidden;
  position: fixed; /* Set the navbar to fixed position */
  top: 0; /* Position the navbar at the top of the page */
  width: 100%;
}
.vf-header-navigation {
  display: flex;
  flex-direction: row;
  font-size: 1.4rem;
  text-decoration: none;
}
.vf-header-item {
  text-decoration: none;
  padding-right: 1rem;
  padding-left: 1rem;
  color: white;
}
</style>
