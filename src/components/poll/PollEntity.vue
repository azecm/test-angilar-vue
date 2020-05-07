<template>
  <form class="poll-entity" ref="entity">
    <div class="col-1">
      <div v-if="index>1" class="operator">или</div>
      {{title}} {{index}}
    </div>
    <div class="col-2">
      <template v-if="type===EType.range">
        от <input type="text" name="from"> до <input type="text" name="to">
      </template>
      <template v-else-if="type===EType.type">
        <select class="entity" name="type">
          <option>Gold</option>
          <option>Silver</option>
        </select>
      </template>
      <template v-else-if="type===EType.status" name="status">
        <select class="entity">
          <option>Активна</option>
          <option>Пассивна</option>
        </select>
      </template>
    </div>
  </form>
</template>

<script lang="ts">

  import {Component, Vue, Prop} from 'vue-property-decorator';
  import {DataPollItemEntity, EType, pollTitles} from "@/components/poll/_common";

  @Component
  export default class PollEntity extends Vue {
    @Prop()
    index!: number;
    @Prop()
    type!: EType;
    @Prop()
    data!: DataPollItemEntity;

    EType = EType;

    get title() {
      return pollTitles[this.type];
    }

    mounted() {
      const form = this.$refs.entity as HTMLFormElement;
      this.data.elements = [...form.elements] as HTMLInputElement[];
    }
  }
</script>

<style scoped lang="scss">
  @import "cols";
  @import "select";
  @import "../../styles/button-drop";

  .poll-entity {
    display: flex;
    margin: 0.3em 0;
  }

  input {
    width: 7em;
    margin: 0 0.5em;
  }

  select.entity {
    width: 90%;
  }
</style>
