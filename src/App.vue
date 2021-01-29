<template>
  <div id="app">
    <h1>To Do List</h1>
    <Add @addToDo = "addNewToDo"/>
    <List v-for="el of arrToDo"
          :key="el.id"
          :elArrInComp="el"
          @delList="deleteList"
          @changeText="changeText"/>

  </div>
</template>

<script>
import Add from "@/components/Add";
import List from "@/components/List";
export default {
  name: 'App',
  components: {
    Add, List
  },
  created() {
    if (localStorage.getItem('arrToDo') ) {
      this.arrToDo = JSON.parse(localStorage.getItem('arrToDo'))
    }
    if (localStorage.getItem('idToDo') ) {
      this.idToDo = JSON.parse(localStorage.getItem('idToDo'))
    }
  },
  data () {
    return {
      arrToDo: [],
      idToDo: 0
    }
  },
  methods: {
    addNewToDo (text) {
      this.arrToDo.push({
        id: this.idToDo++,
        text: text,
        complete: false
      })
      this.setData()
    },
    deleteList (id) {
        for (let i = 0; i < this.arrToDo.length; i++) {
          this.arrToDo[i].id === id ? this.arrToDo.splice(i, 1) : ''
        }
        this.setData()
    },
    changeText (objectList) {
      for (let i = 0; i<this.arrToDo.length; i++) {
        this.arrToDo[i].id === objectList.id ? this.arrToDo.splice(i, 1, objectList) : ''
      }
      this.setData()
    },
    setData () {
      localStorage.setItem('arrToDo', JSON.stringify(this.arrToDo))
      localStorage.setItem('idToDo', JSON.stringify(this.idToDo))
      if (localStorage.getItem('arrToDo') === "[]") {
        localStorage.setItem('idToDo', "0")
        this.idToDo = 0
      }
    }
  }
}
</script>

<style lang="scss">
@import "assets/reset.css";
#app {
  width: 100%;
  min-height: 100vh;
  margin: 0 auto;
  background: linear-gradient(to bottom right, #47393590, #beaea790), url("assets/images/background.jpg") center;
  background-size: cover;
  text-align: center;
  h1 {
    font-size: 50px;
    font-weight: 800;
    font-family: "JetBrains Mono";
    font-style: italic;
    background: linear-gradient(to bottom right, rgba(24, 25, 29, 0.9), rgba(62, 40, 40, 0.9)), url("assets/images/to-do.jpg") center;
    background-size: cover;
    padding: 50px 0;
    color: #fff;
  }
}
</style>
