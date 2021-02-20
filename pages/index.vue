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
      <div class="my-4">
        <b-table-simple>
          <b-tr v-for="tool in tools" :key="tool.id">
            <b-td>
              <nuxt-link :to="tool.link">{{ tool.name }}</nuxt-link>
            </b-td>
            <b-td>{{ tool.description }}</b-td>
          </b-tr>
        </b-table-simple>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  layout: 'no_header',
  data() {
    return {
      tools: [
        {
          name: 'set_number',
          description: 'ソースコードに行番号を付与します。',
          link: '/set_number',
        },
        {
          name: 'canary',
          description: 'SQL の読み仮名を生成します。',
          link: '/canary',
        },
      ],
    }
  },
})
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
