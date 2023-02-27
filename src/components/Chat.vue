<template>
  <div class="position-absolute bottom-0 end-0 m-5">
    <div class="card shadow" style="width: 500px">
      <div class="card-header">AI</div>
      <div class="card-body">
        <p class="card-text h5">Ask me anything</p>
        <div v-if="!init" class="overflow-auto h-80 p-3 mb-3 shadow">
          <p v-if="!loading" class="card-text" style="max-height: 100px">
            <span>{{ answer }}</span>
          </p>
          <p v-else>loading...</p>
        </div>
        <div class="input-group">
          <input type="text" class="form-control" v-model="message" />
          <button
            class="btn btn-outline-secondary"
            type="button"
            v-on:click="ai"
          >
            submit
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      init: true,
      loading: false,
      message: '',
      quiestion: '',
      answer: ''
    }
  },
  methods: {
    ai() {
      let url = 'https://www.leafhomesafetysolutions.com'
      let text =
        "walk-in tubs's link is https://www.leafhomesafetysolutions.com/walk-in-tubs/. walk-in showers link is https://www.leafhomesafetysolutions.com/tub-to-shower/. stair-lifts's link is https://www.leafhomesafetysolutions.com/stair-lifts/"
      this.init = false
      this.loading = true
      let config = {
        method: 'get',
        maxBodyLength: Infinity,
        url: `https://ama-ai.ronsong.xyz/ama_v2?url=${url}&text=${text}&question=${this.message}`,
        headers: {}
      }

      axios(config)
        .then((response) => {
          let data = response.data
          console.log(data)
          this.question = data.question
          this.answer = data.answer
          this.message = ''
          this.loading = false
        })
        .catch((error) => {
          console.log(error)
          this.message = error
        })
    }
  }
}
</script>
