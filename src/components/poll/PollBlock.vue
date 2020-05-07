<template>
  <div class="poll-block">
    <header>Добавить опрос</header>

    <poll-item v-for="(item,i) in items" :key="item.ind" :class="pollItemClassName(i)" :data="item"
               v-on:remove="onRemove"></poll-item>

    <add-condition @click.native="onAdd"></add-condition>
    <footer>
      <button class="button-test" @click="onTest">Протестировать опрос</button>
      <button class="button-next">Далее →</button>
    </footer>
    <result-block v-if="resultData" :data="resultData" @click.native="onTestClose"></result-block>
  </div>
</template>

<script lang="ts">
  import AddCondition from "@/components/poll/AddCondition.vue";
  import PollItem from "@/components/poll/PollItem.vue";
  import ResultBlock from "@/components/poll/ResultBlock.vue";
  import {Component, Vue} from 'vue-property-decorator';
  import {DataPollItem, ResultInterface, pollTypeName, ResItem, TRow} from "./_common";

  @Component({
    components: {AddCondition, PollItem, ResultBlock: ResultBlock}
  })
  export default class PollBlock extends Vue {
    items = [] as DataPollItem[];
    resultData = null as ResultInterface | null;

    onAdd() {
      this.items.push(new DataPollItem());
    }

    onRemove(item: DataPollItem) {
      const pos = this.items.map(i => i.ind).indexOf(item.ind);
      this.items.splice(pos, 1);
    }

    pollItemClassName(ind: number) {
      return `type-${(ind % 4) + 1}`;
    }

    onTestClose() {
      this.resultData = null;
    }

    onTest() {
      const result: ResultInterface = {resultName: 'Опрос', items: [] as ResItem[]};
      for (const item of this.items) {
        if (!item.type || !item.entityList.length) continue;
        const rows = [] as TRow[];
        const resItem = {type: item.type, typeName: pollTypeName[item.type], rows} as ResItem;
        result.items.push(resItem);
        for (const entity of item.entityList) {
          switch (entity.elements.length) {
            case 0: {
              break;
            }
            case 1: {
              rows.push(entity.elements[0].value);
              break;
            }
            default: {
              const row = [] as (string | number)[];
              rows.push(row);
              for (const elem of entity.elements) {
                row.push(elem.value);
              }
              break;
            }
          }
        }
      }
      this.resultData = result;
    }
  }

</script>

<style scoped lang="scss">
  @import "../../styles/colors";
  @import "common";

  .poll-block {
    display: block;
    position: relative;
  }

  header {
    padding: 1em 2em;
    font-weight: bold;
    color: silver;
  }

  footer {
    display: flex;
    justify-content: space-between;
    padding: 1em 2em;
    background-color: #f4f7f9;
  }

  button {
    border-radius: 0.3em;
    padding: 0.5em 1.5em;
    border: 0 none;
    cursor: pointer;
    transition-duration: 0.3s;

    &:focus {
      outline: 0 none;
    }

    &.button-test {
      color: $top-color;
      background-color: white;

      &:hover {
        box-shadow: 0 0 0.3em inset $top-color;
      }
    }

    &.button-next {
      color: white;
      background-color: $top-color;

      &:hover {
        box-shadow: 0 0 0.3em inset white;
      }
    }
  }
</style>

