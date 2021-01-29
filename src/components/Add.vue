<template>
<div id="add">
  <input type="text" v-model="text" @keyup.enter="addToDo">
  <input type="button" value=" " @click="addToDo">
</div>
</template>

<script>
export default {
  name: "Add",
  data () {
    return {
      text: ''
    }
  },
  methods: {
    addToDo () {
      if(this.text) {
        this.$emit('addToDo', this.text)
        this.text = ''
      }
    }
  }
}
</script>

<style lang="scss">

#add {
  margin: 10px auto;
  input {
    padding: 10px;
    font-family: "JetBrains Mono", sans-serif;
    font-size: 18px;
    outline: none;
    &[type="button"] {
      cursor: pointer;
      background: url("../assets/images/plus.svg") no-repeat center, #beaea7;
      background-size: contain;
      min-width: 40px;
    }
  }
}

</style>
