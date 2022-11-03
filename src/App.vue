<script setup>
import {RouterView} from 'vue-router'</script>

<template>
  <div class="header">
    <h1 class="is-size-1 has-text-weight-bold has-text-white">RoR Builder Converter</h1>
    <h5 class="is-size-5 has-text-white">Convert old builder URLs to work on the updated RoR Builder page</h5>
  </div>
  <section class="section mt-6">
    <div class="container">
      <RouterView/>
    </div>
  </section>
</template>

<style scoped lang="scss">
.header {
  width: 100%;
  height: 300px;
  background-image: linear-gradient(0deg, rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url("@/assets/logo.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>