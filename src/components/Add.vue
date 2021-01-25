<template>
<div id="add">
  <input type="text" v-model="text" @keyup.enter="addToDo">
  <input type="button" value="+" @click="addToDo">
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
  background: #a52a2a;
  width: 50%;
  input {
    &[type="button"] {
      cursor: pointer;
    }
  }
}

</style>
