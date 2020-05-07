<template>
  <div class="poll-item">
    <div class="flex">
      <div class="col-1">
        <div class="title">Условие</div>
      </div>
      <div class="col-2">
        <select class="width-100" @change="onChangeType">
          <option :value="EType.none">Выберите условие</option>
          <option :value="EType.range">{{pollTypeName[EType.range]}}</option>
          <option :value="EType.type">{{pollTypeName[EType.type]}}</option>
          <option :value="EType.status">{{pollTypeName[EType.status]}}</option>
        </select>
      </div>
    </div>
    <div class="body">
      <poll-entity v-for="(entity,i) in data.entityList" :key="entity.ind" :index="i+1" :data="entity"
                   :type="type"></poll-entity>
    </div>
    <div class="flex">
      <div class="col-1">

      </div>
      <div class="col-2 flex flex-between">
        <action-button type="add" @click.native="onAddClick">Добавить {{buttonText}}</action-button>
        <action-button type="remove" @click.native="onRemoveClick">Удалить условие</action-button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
  import PollEntity from "@/components/poll/PollEntity.vue";
  import ActionButton from "@/components/element/ActionButton.vue";
  import {DataPollItem, EType, pollTitles, pollTypeName} from './_common';
  import {Component, Vue, Prop} from 'vue-property-decorator';

  @Component({
    components: {ActionButton, PollEntity}
  })
  export default class PollItem extends Vue {
    @Prop()
    data!: DataPollItem;

    //@Model('remove', {type: Boolean}) readonly checked!: boolean
    //@PropSync('data', { type: DataPollItem }) syncedData!: DataPollItem

    pollTypeName = pollTypeName;
    EType = EType;

    get type() {
      return this.data.type;
    }

    get buttonText() {
      return pollTitles[this.type].toLowerCase();
    }

    onChangeType(e: Event) {
      const el = e.target as HTMLSelectElement;
      this.data.type = parseInt(el.value, 10);
      this.onAddClick();
    }

    onAddClick() {
      if (this.data.type) {
        this.data.addEntity();
      }
    }

    onRemoveClick() {
      this.$emit('remove', this.data);
    }
  }
</script>

<style scoped lang="scss">
  @import "common";
  @import "cols";
  @import "select";

  .poll-item {
    display: block;
    padding: 1em 2em;
  }

  $i2: 0;
  @each $background, $title, $operator in $colors {
    $i2: $i2 + 1;
    .poll-item.type-#{$i2}:before {
      background-color: $operator;
    }
  }


  .poll-item {
    &:not(:first-of-type):before {
      display: block;
      position: absolute;
      content: 'и';
      transform: translateY(-2.3em);
      border-radius: 0.2em;
      padding: 0.5em 1em;
      font-size: 0.8rem;
    }
  }


  // ==============

  .body {
    margin: 0.8em 0;
  }

  // ===============

  .flex {
    display: flex;

    &-between {
      justify-content: space-between;
    }
  }

</style>
