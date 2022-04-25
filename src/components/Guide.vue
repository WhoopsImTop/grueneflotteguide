<template>
  <div v-show="modal" class="guide-card" :class="darkmode ? 'dark' : ''">
    <div class="card">
      <div class="guide-card-image">
        <img
          :src="
            darkmode
              ? guideData[index].img + '-dark.svg'
              : guideData[index].img + '.svg'
          "
        />
      </div>
      <div class="guide-card-title">
        <h2>{{ guideData[index].title }}</h2>
      </div>
      <div class="guide-card-content">
        <p>{{ guideData[index].description }}</p>
      </div>
    </div>
    <div class="guide-card-footer">
      <button @click="index--" :disabled="index == 0">zurück</button>

      <div class="dots">
        <div
          class="dot"
          v-for="(dot, i) in guideData"
          @click="index = i"
          :key="i"
          :class="i == index ? 'active' : ''"
        ></div>
      </div>

      <button
        @click="
          index == guideData.length - 1
            ? ((index = 0),
              window.parent.postMessage('infoScreenFinished', '*'))
            : index++
        "
      >
        {{ index == guideData.length - 1 ? "Los geht's" : "nächste" }}
      </button>
    </div>
  </div>
</template>

<script>
import readJsonData from "../helpers/readJsonData.js";
export default {
  name: "GuideComponent",
  props: ["modal"],
  data() {
    return {
      index: 0,
      guideData: [],
      darkmode: false,
      startX: 0,
      endX: 0,
    };
  },
  methods: {
    addDragListener() {
      let card = document.querySelector(".card");
      card.addEventListener("touchstart", (e) => {
        this.startX = e.changedTouches[0].clientX;
      });
      card.addEventListener("touchend", (e) => {
        this.endX = e.changedTouches[0].clientX;
        if (this.endX - this.startX > 0) {
          if(this.index > 0) {
          this.index--;
          }
        } else {
          if(this.index < this.guideData.length - 1) {
          this.index++;
          }
        }
      });      
    },
  },
  beforeMount() {
    this.guideData = readJsonData();
    //check for device darkmode
    if (
      window.matchMedia &&
      window.matchMedia("(prefers-color-scheme: dark)").matches
    ) {
      this.darkmode = true;
    }
  },
  created() {
    window.addEventListener("DOMContentLoaded", this.addDragListener);
  },
};
</script>

<style>
.guide-card.dark {
  background-color: #222222;
}
.dark .guide-card-title h2 {
  color: #efefef;
  text-align: center;
}
.dark .guide-card-content {
  color: #d1d1d1;
}

.guide-card {
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
  margin-bottom: 20px;
  padding: 40px;
  max-width: 280px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.guide-card-image {
  height: 180px;
  margin-bottom: 30px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.guide-card-title {
  padding: 0;
  margin: 0;
  text-transform: uppercase;
  letter-spacing: 2px;
  text-align: center;
}

.guide-card-divider {
  margin: 15px 0 10px;
  border: 1px solid #efefef;
}

.guide-card-content {
  text-align: center;
  font-size: 16px;
  color: #444444;
  height: 120px;
  margin-bottom: 20px;
}

.guide-card-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}

.dots {
  display: flex;
  justify-content: center;
  align-items: center;
}

.dot {
  width: 15px;
  height: 2px;
  background-color: #d1d1d1;
  margin: 0 2.5px;
  transition: 0.3s;
}

.dot.active {
  background-color: #83bb26;
  width: 25px;
}

button {
  border: none;
  outline: none;
  background-color: transparent;
  color: #83bb26;
  font-size: 14px;
  letter-spacing: 1px;
  font-family: Open-Sans, sans-serif;
}

button:disabled {
  color: #ccc;
}

.dark button:disabled {
  color: #858585;
}

h2 {
  font-size: 20px;
  margin: 0;
  font-weight: bold;
}
</style>
