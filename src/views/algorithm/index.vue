<template>
  <div class="pd-24">
    <div>
      <el-input
        v-model="textarea"
        type="textarea"
        :rows="3"
        placeholder="请输入内容"
        maxlength="100"
        show-word-limit
        class="mg-b-16"
      />
      <el-button type="primary" @click="submit">提 交</el-button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Index',
  data() {
    return {
      textarea: ''
    }
  },
  created() {
    this.submit = this.debounce(this.submit)
  },
  methods: {
    debounce(cb, delay = 1000) {
      let timer = 0
      return function() {
        if (timer) {
          clearTimeout(timer)
        }
        timer = setTimeout(() => {
          console.log(arguments)
          cb.apply(this, arguments)
        }, delay)
      }
    },
    submit() {
      console.log(this.textarea)
    }
  }
}
</script>

<style scoped>

</style>
