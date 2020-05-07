<template>
  <div class="add-condition">
    <button>
      <svg focusable="false" data-prefix="fal" data-icon="plus" xmlns="http://www.w3.org/2000/svg"
           viewBox="0 0 384 512">
        <path fill="currentColor"
              d="M376 232H216V72c0-4.42-3.58-8-8-8h-32c-4.42 0-8 3.58-8 8v160H8c-4.42 0-8 3.58-8 8v32c0 4.42 3.58 8 8 8h160v160c0 4.42 3.58 8 8 8h32c4.42 0 8-3.58 8-8V280h160c4.42 0 8-3.58 8-8v-32c0-4.42-3.58-8-8-8z"></path>
      </svg>
      <div>
        Нажмите, чтобы добавить новое условие выборки.<br>
        Все условия связываются между собой логическим "И"
      </div>
    </button>
  </div>
</template>

<script lang="ts">
  import {Component, Vue} from 'vue-property-decorator';

  @Component
  export default class AddCondition extends Vue {
  }
</script>

<style scoped lang="scss">
  @import "../../styles/colors";
  @import "../../styles/button-drop";

  .add-condition {
    display: flex;
    padding: 1em 2em;
  }

  svg {
    height: 2em;
    width: auto;
    pointer-events: none;
  }

  button {
    color: $top-color;
    border-radius: 0.5em;
    cursor: pointer;
    background-color: transparent;
    border: 1px solid $add-color;
    text-align: center;
    padding: 1em;
    transition-duration: 0.3s;
    flex-grow: 1;

    &:hover {
      border-color: $top-color;
      box-shadow: 0 0 0.3em inset $top-color;
    }
  }
</style>
