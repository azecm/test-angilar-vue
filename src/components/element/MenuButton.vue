<template>
  <button>
    <slot></slot>
  </button>
</template>

<script lang="ts">
  import {Component, Vue} from 'vue-property-decorator';

  @Component
  export default class MenuButton extends Vue {
  }
</script>

<style scoped lang="scss">
  @import "../../styles/colors";
  @import "../../styles/button-drop";

  button {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 90%;
    margin: 0.5em 0;
    border-radius: 0.5em;
    border: 1px solid transparent;
    padding: 0.8em 0.2em;
    cursor: pointer;
    color: black;
    transition-duration: 0.3s;
    transition-property: color, border-color;
    background-color: transparent;

    &.active {
      background-color: $active-back;
    }

    &:hover {
      color: $add-color;
      border-color: $add-color;
    }
  }

  svg {
    pointer-events: none;
    height: 2em;
    width: auto;
    margin-bottom: 0.5em;
  }
</style>
