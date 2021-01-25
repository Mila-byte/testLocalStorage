<template>
<div id="list">
  <input type="text" :readonly="editMode" v-model="text">
  <input type="button" value="X" @click="showModal=true">
  <input type="button" :value="editMode ? 'Change' : 'Save'" @click="changeText">
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
  data () {
    return {
      showModal: false,
      editMode: true,
      text: this.elArrInComp.text
    }
  },
  methods: {
    deleteElArr () {
      this.$emit('delList', this.elArrInComp.id)
    },
    changeText() {
      !this.editMode ? this.$emit('changeText', {id: this.elArrInComp.id, text: this.text}) : ''
      this.editMode = !this.editMode
    }
  }
}
</script>

<style lang="scss">

#list{
  margin: 10px 0;
  input {
    padding: 10px;
    &[type="button"] {
      cursor: pointer;
      background: #a52a2a99;
      color: #e3d0d7;
    }
  }
}

</style>
