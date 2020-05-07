<template>
  <button :class="buttonClassName">
    <svg v-if="isAdd" focusable="false" data-prefix="fas" data-icon="plus" xmlns="http://www.w3.org/2000/svg"
         viewBox="0 0 448 512">
      <path fill="currentColor"
            d="M416 208H272V64c0-17.67-14.33-32-32-32h-32c-17.67 0-32 14.33-32 32v144H32c-17.67 0-32 14.33-32 32v32c0 17.67 14.33 32 32 32h144v144c0 17.67 14.33 32 32 32h32c17.67 0 32-14.33 32-32V304h144c17.67 0 32-14.33 32-32v-32c0-17.67-14.33-32-32-32z"></path>
    </svg>
    <svg v-if="isRemove" focusable="false" data-prefix="far" data-icon="trash-alt"
         xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512">
      <path fill="currentColor"
            d="M268 416h24a12 12 0 0 0 12-12V188a12 12 0 0 0-12-12h-24a12 12 0 0 0-12 12v216a12 12 0 0 0 12 12zM432 80h-82.41l-34-56.7A48 48 0 0 0 274.41 0H173.59a48 48 0 0 0-41.16 23.3L98.41 80H16A16 16 0 0 0 0 96v16a16 16 0 0 0 16 16h16v336a48 48 0 0 0 48 48h288a48 48 0 0 0 48-48V128h16a16 16 0 0 0 16-16V96a16 16 0 0 0-16-16zM171.84 50.91A6 6 0 0 1 177 48h94a6 6 0 0 1 5.15 2.91L293.61 80H154.39zM368 464H80V128h288zm-212-48h24a12 12 0 0 0 12-12V188a12 12 0 0 0-12-12h-24a12 12 0 0 0-12 12v216a12 12 0 0 0 12 12z"></path>
    </svg>
    <span class="text">
        <slot></slot>
    </span>
  </button>
</template>

<script lang="ts">

  import {Component, Prop, Vue} from 'vue-property-decorator';

  @Component
  export default class ActionButton extends Vue {
    @Prop()
    type!: 'add' | 'remove';

    get buttonClassName() {
      return `type-${this.type} button`;
    }

    get isAdd() {
      return this.type == 'add';
    }

    get isRemove() {
      return this.type == 'remove';
    }
  }
</script>

<style scoped lang="scss">
  @import "../../styles/colors";
  @import "../../styles/button-drop";

  .button {
    display: inline-flex;
    align-items: center;
    padding: 0.4em 0.6em;
    border-style: solid;
    border-width: 1px;
    border-radius: 0.3em;
    background-color: white;
    outline: 0 none;
    cursor: pointer;
    transition-duration: 0.3s;
    transition-property: color, border-color, box-shadow;

    &:focus, &:active {
      outline: 0 none;
    }
  }

  svg {
    pointer-events: none;
    height: 1em;
    width: auto;
  }

  .type-add {
    border-color: $add-color;
    color: $add-color;

    &:hover {
      border-color: $add-color-hover;
      color: $add-color-hover;
      box-shadow: 0 0 0.3em inset $add-color;
    }
  }

  .type-remove {
    border-color: $remove-color;
    color: $remove-color;

    &:hover {
      border-color: $remove-color-hover;
      color: $remove-color-hover;
      box-shadow: 0 0 0.3em inset $remove-color;
    }
  }

  .text {
    margin-left: 0.5em;
  }
</style>
