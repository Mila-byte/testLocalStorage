<template>
  <div id="list">
    <input type="text" :readonly="editMode" v-model="text">
    <input type="button" class="done"
           :class="{
    statusClick: complete
  }"
           value=" " @click="completeTask">
    <input type="button" class="delete" value="X" @click="showModal=true">
    <input type="button" class="change" :value="editMode ? 'Change' : 'Save'" @click="changeText">
    <ModalWindow
        v-show="showModal"
        @declineDelete="showModal=false"
        @deleteList="deleteElArr"/>
  </div>
</template>

<script>
import ModalWindow from "@/components/ModalWindow";

export default {
  name: "List",
  components: {ModalWindow},
  props: [
    'elArrInComp'
  ],
  data() {
    return {
      showModal: false,
      editMode: true,
      text: this.elArrInComp.text,
      complete: this.elArrInComp.complete
    }
  },
  methods: {
    deleteElArr() {
      this.$emit('delList', this.elArrInComp.id)
    },
    changeText () {
      !this.editMode ? this.$emit('changeText', {id: this.elArrInComp.id, text: this.text, complete: this.complete}) : ''
      this.editMode = !this.editMode
    },
    completeTask () {
      this.complete = !this.complete
      this.$emit('changeText', {id: this.elArrInComp.id, text: this.text, complete: this.complete})
    }
  }
}
</script>

<style lang="scss">

#list {
  margin: 10px 0;

  input {
    font-family: "JetBrains Mono", sans-serif;
    font-size: 18px;
    padding: 10px;

    &[type="button"].delete {
      cursor: pointer;
      background: #8a665e;
      color: #ae2a37;
      font-weight: 600;
    }

    &[type="button"].change {
      cursor: pointer;
      background: #8a665e;
      color: #1d1413;
      font-weight: 600;
    }

    &[type="button"].done {
      outline: none;
      cursor: pointer;
      background: url("../assets/images/Checkmark.png") no-repeat center;
      background-size: contain;
      &.statusClick {
        background: radial-gradient(transparent, #07e35380), url("../assets/images/Checkmark.png") no-repeat center;
        background-size: contain;
        border: 2px solid #07e55580;
      }
    }


  }
}

</style>
