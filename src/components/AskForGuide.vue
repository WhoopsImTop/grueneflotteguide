<template>
  <div v-show="modal" class="welcomeguide-card" :class="darkmode ? 'dark' : ''" >
    <div class="welcomeguide-card-image">
      <img :src="darkmode ? 'static/logo-dark.png' : 'static/logo.png'" />
    </div>
    <div class="welcomeguide-card-title">
      <h2>Grüne Flotte Carsharing</h2>
    </div>
    <div class="welcomeguide-card-content">
      <p>Wir haben was du suchst!</p>
    </div>
    <div class="welcomeguide-card-footer">
        <button class="primary" @click="$emit('openModal')">Tour starten</button>
        <button class="secondary" @click="$emit('closeAskModal')">Überspringen</button>
        <label><input type="checkbox" v-model="showNextTime">Beim nächsten Start nicht mehr anzeigen</label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'AskComponent',
  props: ["modal"],
  data() {
    return {
      darkmode: false,
      showNextTime: false,
    }
  },
  beforeMount () {
    if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
      this.darkmode = true;
    }
  },
}
</script>

<style>

  .welcomeguide-card.dark {
    background-color: #222222;
  }
  .dark .welcomeguide-card-title h2 {
    color: #efefef;
  }
  .dark .welcomeguide-card-content {
    color: #D1D1D1;
  }

  .welcomeguide-card {
    background-color: #fff;
    border-radius: 10px;
    box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
    margin-bottom: 20px;
    padding: 40px;
    max-width: 280px;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
  }

  .welcomeguide-card-image {
    height: 100px;
    margin-bottom: 30px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .welcomeguide-card-title {
    padding: 0;
    margin: 0;
    text-transform: uppercase;
    letter-spacing: 2px;
  }

  .welcomeguide-card-content {
    text-align: center;
    font-size: 16px;
    color: #444444;
    margin-bottom: 20px;
  }

  .welcomeguide-card-footer {
    display: flex;
    flex-direction: column;
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
    background-color: #D1D1D1;
    margin: 0 2.5px;
    transition: .3s;
  }

  .dot.active {
    background-color: #83BB26;
    width: 25px;
  }

  .welcomeguide-card-footer button {
    width: 100%;
    padding: 10px 20px;
    margin: 5px 0;
    border: none;
    outline: none;
    background-color: transparent;
    color: #83BB26;
    font-size: 14px;
    letter-spacing: 1px;
    font-family: Open-Sans, sans-serif;
    text-transform: uppercase;
  }

  .primary {
      background-color: #83BB26 !important;
      color: #ffffff !important;
      font-weight: bolder;;
  }
  
  .secondary {
      background-color: #efefef;
      color: #353535;
  }

  .dark .secondary {
    background-color: #353535;
    color: #ffffff;
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

  label {
    font-size: 13px;
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 10px 0 0 0;
  }

  .dark label {
      color: #D1D1D1;
  }

  [type="checkbox"] {
      width: 20px;
      height: 20px;
  }
</style>
