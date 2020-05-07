<template>
  <div class="user-icon">
    <div class="image" :style="{backgroundImage:src}"></div>
    <div>
      <div class="user">{{user}}</div>
      <div class="role">{{role}}</div>
    </div>
  </div>
</template>

<script lang="ts">

  import {Component, Vue, Prop} from 'vue-property-decorator';

  @Component
  export default class UserIcon extends Vue {

    @Prop()
    user!: string;
    @Prop()
    role!: string;
    @Prop()
    image!: string;

    get src() {
      // eslint-disable-next-line @typescript-eslint/no-var-requires
      const src = require(`@/assets/${this.image}`);
      return `url("${src}")`;
    }


  }
</script>

<style scoped lang="scss">
  .user-icon {
    display: flex;
    align-items: center;
    margin-left: 1em;
    margin-right: 0.3em;
  }

  .image {
    display: block;
    width: 3em;
    height: 3em;
    border-radius: 50%;
    background-size: contain;
    margin-right: 0.5em;
  }

  .user {
    font-weight: bold;
  }
</style>
