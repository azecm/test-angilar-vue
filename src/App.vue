<template>
  <div class="page-vew">
    <LeftBlock></LeftBlock>
    <ContentBlock></ContentBlock>
  </div>
</template>

<script lang="ts">
  import {Component, Vue} from 'vue-property-decorator';
  import LeftBlock from './components/page/LeftBlock.vue';
  import ContentBlock from './components/page/ContentBlock.vue';

  @Component({
    components: {
      LeftBlock,
      ContentBlock
    },
  })
  export default class App extends Vue {
  }
</script>

<style lang="scss">
  body {
    margin: 0;
    padding: 0;
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  .page-vew {
    max-width: 900px;
    margin: auto;
    display: flex;
    box-shadow: 0 0 0.5em #eee;
  }
</style>
