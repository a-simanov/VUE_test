<template>
  <div>
    <div class="container column">
      <ResumeForm @add-block="addBlock"></ResumeForm>
      <ResumeView :blocks="blocks"></ResumeView>
    </div>
    <div class="container">
      <AppLoader v-if="loader"></AppLoader>
      <ResumeComments v-else :comments="comments" @load-comments="loadComments"></ResumeComments>
    </div>
  </div>
</template>

<script>
import ResumeForm from './components/AppForm.vue'
import ResumeView from './components/AppBlocks.vue'
import ResumeComments from './components/AppComments'
import AppLoader from './components/AppLoader.vue'

export default {
  data () {
    return {
      loading: false,
      comments: [],
      blocks: []
    }
  },
  methods: {
    async loadComments() {
      this.loading = true
      const res = await fetch('https://jsonplaceholder.typicode.com/comments?_limit=42')
      this.comments = await res.json()
      console.log(this.comments)
      this.loading = false
    },
    addBlock (block) {
      this.blocks.push(block)
    }
  },
  components: {ResumeForm,  ResumeView, ResumeComments, AppLoader}
}
</script>