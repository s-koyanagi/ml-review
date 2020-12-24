<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        機械学習設計書レビュー試用版
      </div>
    </v-app-bar>

    <v-content>
      <HelloWorld />
    </v-content>
    <v-footer absolute>
      <v-col class="text-center" cols="12">
        {{ new Date().getFullYear() }} —
        <strong>Machine learning review team</strong>
      </v-col>
    </v-footer>
  </v-app>
</template>

<script lang="ts">
import Vue from 'vue'
import HelloWorld from './components/HelloWorld.vue'

export default Vue.extend({
  name: 'App',

  components: {
    HelloWorld
  },

  data: () => ({})
})
</script>
