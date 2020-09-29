<template>
  <div class="add_button" @click="onClick">
      <div class="add_icon"></div>
  </div>
</template>

<script>
  export default {
    name: "AddButton",
    methods: {
      onClick() {
        this.$emit('addStopwatch')
      },
    }
  }
</script>

<style scoped lang="scss">
  $enabled: #fff;
  $disabled: #9E9E9E;
  $background: #696969;

  .add_ {
    &button {
      width: 225px;
      height: 120px;
      background: $background;
      display: flex;
      justify-content: center;
      align-items: center;
      &:hover .add_icon {
        &:after, &:before {
          background-color: $enabled;
        }
      }
    }
    &icon {
      position: relative;
      width: 20px;
      height: 20px;
      &:before {
        content: '';
        position: absolute;
        height: 20px;
        width: 3px;
        top: 0;
        left: 10px - 1.5px;
        background-color: $disabled;
      }
      &:after {
        content: '';
        position: absolute;
        width: 20px;
        height: 3px;
        top: 10px - 1.5px;
        left: 0;
        background-color: $disabled;
      }
    }
  }



</style>