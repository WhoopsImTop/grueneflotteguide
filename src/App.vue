<template>
  <AskForGuideComponent :modal="askModal" @openModal="modal = true, askModal = false" @closeAskModal="askModal = false"/>
  <GuideComponent :modal="modal" @closeModal="modal = false"/>
  <RetryComponent :modal="(modal != true && askModal != true) ? true : false" @resetModals="resetAllModalData()"/>
</template>

<script>
import GuideComponent from './components/Guide.vue'
import AskForGuideComponent from './components/AskForGuide.vue'
import RetryComponent from './components/Retry.vue'

export default {
  name: 'App',
  data() {
    return {
      modal: false,
      askModal: true,
    }
  },
  components: {
    GuideComponent,
    AskForGuideComponent,
    RetryComponent,
  },
  methods: {
    resetAllModalData() {
      this.modal = false;
      this.askModal = true;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Open Sans', sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 97vh;
}
</style>
