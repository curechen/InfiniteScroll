<template>
  <ul>
    <li v-for="(item) in searchArr" :key="item">
      {{item}}
    </li>
  </ul>
  <InfiniteScroll @add="addEvent"/>
</template>

<script>
import InfiniteScroll from './components/InfiniteScroll.vue'


export default {
  name: 'App',
  components: {
    InfiniteScroll
  },
  data() {
    return {
      searchArr: [1,2,3,4,5,6,7,8,9,10]
    }
  },
  methods: {
    addEvent() {
      console.log('触发')
      this.searchArr.push(1111)
      console.log(this.searchArr)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0;
  padding: 0;
}
li {
  list-style: none;
  height: 100px;
  background-color: pink;
}

</style>
