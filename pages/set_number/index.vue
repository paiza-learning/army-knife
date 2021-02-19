<template>
  <b-container>
    <h1>:set number</h1>
    <p>行番号つけるやつ</p>

    <b-row>
      <b-col md="6" sm="12">
        <textarea v-model="code" class="form-control" rows="15"></textarea>
      </b-col>
      <b-col md="6" sm="12">
        <textarea
          :value="numbered"
          class="form-control"
          rows="15"
          readonly
        ></textarea>
      </b-col>
    </b-row>
  </b-container>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  data() {
    return {
      code:
        '祇園精舎の鐘の声、諸行無常の響きあり。\n沙羅双樹の花の色、盛者必衰の理をあらはす。\n奢れる人も久からず、ただ春の夜の夢のごとし。\n猛き者も遂にはほろびぬ、偏ひとへに風の前の塵におなじ。',
    }
  },
  computed: {
    numbered() {
      const codes = this.code.split('\n')
      const length = codes.length < 100 ? 2 : 3

      const numbered: string[] = []
      codes.forEach((c, i) => {
        const num = `00${i + 1}`.slice(-length)
        numbered.push(`${num}: ${c}`)
      })

      return numbered.join('\n')
    },
  },
})
</script>
