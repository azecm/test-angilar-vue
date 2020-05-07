<template>
  <div class="tab-button">
    <button>
      <slot></slot>
    </button>
  </div>

</template>

<script lang="ts">
  import {Component, Vue} from 'vue-property-decorator';

  @Component
  export default class TabButton extends Vue {
  }
</script>

<style scoped lang="scss">
  @import "../../styles/colors";
  @import "../../styles/button-drop";

  .tab-button {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    height: 2em;
    flex-grow: 1;

    &#{$active} {
      color: black;
      font-weight: bold;
      border-bottom: 2px solid $add-color;
    }

    &:not(#{$active}) {
      color: $top-color;
    }

    &:hover:not(#{$active}) {
      border-bottom: 2px solid $active-back;
    }

    &:hover {
      background-color: $active-back;
    }
  }

  button {
    height: 100%;
    width: 100%;
    background-color: transparent;
    border: 0 none;
    cursor: pointer;
    color: inherit;
    font-weight: inherit;
  }
</style>
