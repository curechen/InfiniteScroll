<template>
  <div class="container" ref="item">
    <ul class="strip-loading">
      <li style="--line-index: 1"></li>
      <li style="--line-index: 2"></li>
      <li style="--line-index: 3"></li>
      <li style="--line-index: 4"></li>
      <li style="--line-index: 5"></li>
      <li style="--line-index: 6"></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "InfiniteScroll",
  data() {
    return {
      flag: false,
    }
  },
  mounted() {
    let item = this.$refs.item
    console.log(item)
    var io = new IntersectionObserver(
      (entries) => {
        entries.forEach((item) => {
          if (item.isIntersecting) {
            if (!this.flag) {
              this.flag = true
              console.log("触发无限滚动")
              setTimeout(() => {
                this.$emit("add")
                this.flag = false
              }, 2000)
            }
          }
        })
      },
      {
        root: null,
        threshold: 0, // 阀值设为1，当只有比例达到1时才触发回调函数
      }
    )

    io.observe(item)
  },
  methods: {
    fn(e) {
      this.$emit("update:title", e.target.value)
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.strip-loading {
  display: flex;
  justify-content: center;
  align-items: center;
  /* width: 100px; */
  /* height: 100px; */
}

.strip-loading li {
  --time: calc((var(--line-index) - 1) * 200ms);
  border-radius: 3px;
  width: 4px;
  height: 20px;
  background-color: #33cc99;
  animation: beat 1.2s ease-in-out var(--time) infinite;
  list-style-type: none;
}

li + li {
  margin-left: 5px;
}

@keyframes beat {
  0%,
  100% {
    transform: scaleY(1);
  }
  50% {
    transform: scaleY(0.5);
  }
}
</style>
