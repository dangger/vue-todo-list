<template>
  <div id="app">
    <h1 v-text="title" />
    <h5 v-text="description" />
    <input v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
      <li v-for="item in items" v-bind:class="{finished: item.isFinished}" v-on:click="toggleFinish(item)">
        {{item.label}}
      </li>
    </ul>
  </div>
</template>

<script>
import Store from './store'
console.log(Store)
export default {
  data:function () {
    return {
      title: 'TODO LIST',
      description: '使用vue.js和localstorage实现的简单TODO LIST',
      items: Store.fetch(),
      newItem: ''
    }
  },
  watch: {
    items: {
      handler:function (items) {
        Store.save(items)
      },
      deep: true
    }
  },
  methods: {
      toggleFinish:function (item) {
       item.isFinished = !item.isFinished
      },
      addNew:function () {
        this.items.push({
          label: this.newItem,
          isFinished: false
        })
        this.newItem = ''
      }
  }
}
</script>

<style>
.finished{
  text-decoration: line-through;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
