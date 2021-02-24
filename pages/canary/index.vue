<template>
  <b-container>
    <h1>canary</h1>
    <p>SQL の読み仮名を生成します。</p>

    <textarea v-model="query" class="form-control" rows="15"></textarea>
    <textarea :value="yomi" class="form-control" rows="10" readonly> </textarea>

    <h2>使用上の注意</h2>
    <ul>
      <li>
        以下のコーディング規約に沿っていない場合は、読み仮名が生成されません。
        <ul>
          <li>SQL のキーワードは大文字</li>
          <li>テーブル名・カラム名は小文字</li>
        </ul>
      </li>
    </ul>
  </b-container>
</template>

<script lang="ts">
import Vue from 'vue'

import dictJson from '@/assets/canary.json'

export default Vue.extend({
  data() {
    return {
      dict: new Map(),
      query: 'SELECT COUNT(*) FROM customer;',
    }
  },
  computed: {
    yomi(): string {
      const sql = this.query
        .replace(/\r?\n/g, ' ')
        .replace(/ +/g, ' ')
        .replace(/;/, '')

      const tmp = []
      for (const line of sql.split(' ')) {
        if (line.substr(0, 1) === "'") {
          const content = line.substr(1, line.length - 2)
          tmp.push(this.dict.get("'"))
          tmp.push(this.dict.get(content) || content)
        } else if (line.substr(0, 1) === '(') {
          const content = line.substr(1, line.length - 2)
          tmp.push(this.dict.get('('))
          tmp.push(this.dict.get(content) || content)
        } else if (line.includes('.')) {
          const sp = line.split('.')
          tmp.push(this.dict.get(sp[0]))
          tmp.push(this.dict.get('.'))
          tmp.push(this.dict.get(sp[1]))
        } else if (line.includes('(')) {
          const sp = line.split('(')
          tmp.push(this.dict.get(sp[0]))
          tmp.push(this.dict.get('('))
          tmp.push(this.dict.get(sp[1].substr(0, sp[1].length - 1)))
        } else {
          tmp.push(this.dict.get(line) || line)
        }
      }
      return tmp.join('... ')
    },
  },
  created() {
    for (const d of Object.values(dictJson.sql)) {
      for (const [k, v] of Object.entries(d)) {
        this.dict.set(k, v)
      }
    }
  },
})
</script>
