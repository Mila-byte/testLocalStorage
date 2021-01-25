<template>
<div id="modal">
  <div class="text">
    <p>Confirm deletion?</p>
    <input type="button" value="OK" @click="deleteList">
    <input type="button" value="No" @click="$emit('declineDelete')">
  </div>
</div>
</template>

<script>
export default {
name: "ModalWindow",
  methods: {
  deleteList () {
    this.$emit('deleteList')
  }
  }
}
</script>


<style lang="scss">
#modal{
  width: 100%;
  height: 100%;
  background: #130b0b95;
  position: fixed;
  left: 0;
  top: 0;

  .text {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 200px;
    background: #f0f8ff;
    text-align: right;
    padding: 20px;
    input[type='button'] {
      cursor: pointer;
    }
    p {
      text-align: center;
      margin: 10px 0 30px;
      font-size: 20px;
    }
  }
}
</style>
