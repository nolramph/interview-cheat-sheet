<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" height="150" width="150"/>
    <PanelView />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import PanelView from "./PanelView.vue";

export default defineComponent({
  name: "HomeView",
  components: {
    PanelView
  },
});
</script>

<style>
.home img{
  border-radius: 5px;
}
</style>
