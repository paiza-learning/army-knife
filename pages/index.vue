<template>
  <div class="hero">
    <div>
      <Logo />
      <h1 class="display-1 border-bottom border-success">army-knife</h1>
      <p class="lead">created by paiza-learning</p>
      <b-alert variant="success" show>
        paiza-learning学生スタッフの作っている便利な業務効率化webアプリ集です。
        <br />誰でも利用することができますが、業務の都合で予告なしに挙動を変更することがあります。
      </b-alert>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({})
</script>

<style>
.hero {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
</style>
