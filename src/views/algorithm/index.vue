<template>
  <div class="pd-24">
    <div>
      <div v-show="visible">一个啊啊啊啊啊啊啊啊啊啊div</div>
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
      textarea: '',
      visible: false
    }
  },
  created() {
    this.submit = this.debounce(this.submit)
    this.onMouseMove = this.throttle(this.onMouseMove)
    window.onmousemove = this.onMouseMove
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
    throttle(cb, delay = 1000) {
      let timer = 0
      return function() {
        if (timer) {
          return
        }
        timer = setTimeout(() => {
          cb.apply(this, arguments)
          timer = null
          // const date = new Date()
          // console.log(date.getHours() + ':' + date.getMinutes() + ':' + date.getSeconds())
        }, delay)
      }
    },
    isInViewPortOfOne(el) {
      // viewPortHeight 兼容所有浏览器写法
      const viewPortHeight = window.innerHeight || document.documentElement.clientHeight || document.body.clientHeight
      const offsetTop = el.offsetTop
      const scrollTop = document.documentElement.scrollTop
      const top = offsetTop - scrollTop
      return top <= viewPortHeight
    },
    isInViewPort(element) {
      const viewWidth = window.innerWidth || document.documentElement.clientWidth
      const viewHeight = window.innerHeight || document.documentElement.clientHeight
      const {
        top,
        right,
        bottom,
        left
      } = element.getBoundingClientRect()

      return (
        top >= 0 &&
        left >= 0 &&
        right <= viewWidth &&
        bottom <= viewHeight
      )
    },
    submit() {
      console.log(this.textarea)
      this.visible = !this.visible
    },
    onMouseMove(event) {
      const e = event || window.event
      console.log('x', e.clientX, 'y', e.clientY)
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  flex-wrap: wrap;
}
.target {
  margin: 5px;
  width: 20px;
  height: 20px;
  background: red;
}
</style>
