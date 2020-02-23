<template>
  <div>
    <video-background :src="videUrl.video_url" style="height: 100vh;
">
      <div class="vf-header">
        <h1>
          <nuxt-link class="vf-header-item" to="/work">Logo</nuxt-link>
        </h1>
        <ul class="vf-header-navigation">
          <nuxt-link class="vf-header-item" to="/work">Work</nuxt-link>/
          <nuxt-link class="vf-header-item" to="/about_us">About us</nuxt-link>
        </ul>
      </div>
      <div class="vf-bottom-information">
        <div class="vf-bottom-information-list">
          <ul>
            <li
              v-for="n in LIST_OF_VIDEOS.length"
              :key="n"
              :class="['vf-list-of-id', {'is-selected': n-1 === videoIndex }]"
            >#{{ showNumber(n) }}</li>
          </ul>
        </div>
        <div class="vf-bottom-information-info">
          <p class="vf-client-name-homepage">{{videUrl.clientName}}</p>
          <p class="vf-client-name-title">{{videUrl.title}}</p>
          <p class="vf-client-name-year">{{videUrl.year}}</p>
        </div>
      </div>
    </video-background>
  </div>
</template>
<script>
import Header from "./../components/header";
import { LIST_OF_VIDEOS, HOME_PAGE_VIDEOS } from "../core/constants";
import debounce from "lodash.debounce";

export default {
  components: {
    Header
  },
  data() {
    return {
      LIST_OF_VIDEOS,
      videoIndex: 0,
      renderComponent: true
    };
  },
  computed: {
    videUrl() {
      this.forceRerender();
      return LIST_OF_VIDEOS[this.videoIndex];
    }
  },
  methods: {
    forceRerender() {
      // Remove my-component from the DOM
      this.renderComponent = false;

      this.$nextTick(() => {
        // Add the component back in
        this.renderComponent = true;
      });
    },
    nextVideo() {
      this.videoIndex++;
      this.$forceUpdate();
    },
    doScroll: function(e) {
      e = window.event || e;
      var delta = Math.max(-1, Math.min(1, e.wheelDelta || -e.detail));
      this.changeSlide(delta);
      e.preventDefault();
    },

    showNumber(number) {
      return number > 10 ? number : `0${number}`;
    },

    setSlide(value) {
      const tempIndex = this.videoIndex + value;
      const maxIndexInArray = this.LIST_OF_VIDEOS.length - 1;
      if (this.videoIndex === 0 && value === -1) {
        this.videoIndex = maxIndexInArray;
      } else if (this.videoIndex === maxIndexInArray && value === 1) {
        this.videoIndex = 0;
      } else {
        this.videoIndex += value;
      }
      this.forceRerender();
    }
  },
  mounted() {
    this.changeSlide = debounce(function(value) {
      this.setSlide(value);
    }, 500);
    if (window.addEventListener) {
      window.addEventListener("mousewheel", this.doScroll.bind(this), {
        passive: false
      });
      window.addEventListener("onwheel", this.doScroll.bind(this), {
        passive: false
      });

      window.addEventListener("DOMMouseScroll", this.doScroll, {
        passive: false
      });
    } else {
      window.attachEvent("onmousewheel", this.doScroll, { passive: false });
    }
  },
  destroyed: function() {
    window.removeEventListener("onmousewheel", this.doScroll);
  }
};
</script>

<style scoped>
@font-face {
  font-family: "BebasNeue";
  src: url("./../static/fonts/BebasNeue.otf");
  font-weight: normal;
  font-style: normal;
}
body {
  font-family: "BebasNeue";
}
.vf-header {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  top: 0;
  height: 5rem;
  width: 100%;
  background: transparent;
  color: white;
  line-height: 0.5rem;
  padding: 2.4rem;
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
.vf-bottom-information {
  position: absolute;
  bottom: 5rem;
  display: flex;
  direction: row;
  margin-left: 1rem;
}
.vf-bottom-information-info {
  margin-left: 3rem;
}
.vf-bottom-information-list li {
  list-style-type: none;
}
.is-selected {
  color: orange !important;
}
.vf-client-name-homepage {
  display: block;
  font-size: 1.5rem;
  color: white;
}
.vf-client-name-year {
  display: block;
  font-size: 1.5rem;
  color: white;
}
.vf-client-name-title {
  display: block;
  font-size: 6rem;
  color: white;
}
.vf-list-of-id {
  margin-bottom: 0.5rem;
  color: grey;
}
/* Style the video: 100% width and height to cover the entire window */
#myVideo {
  position: fixed;
  right: 0;
  bottom: 0;
  min-width: 100%;
  min-height: 100%;
}

/* Add some content at the bottom of the video/page */
.content {
  position: fixed;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  color: #f1f1f1;
  width: 100%;
  padding: 20px;
}

/* Style the button used to pause/play the video */
#myBtn {
  width: 200px;
  font-size: 18px;
  padding: 10px;
  border: none;
  background: #000;
  color: #fff;
  cursor: pointer;
}

#myBtn:hover {
  background: #ddd;
  color: black;
}
</style>
