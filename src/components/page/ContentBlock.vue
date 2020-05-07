<template>
  <div class="content-block">
    <div class="row">
      <input-search></input-search>
      <user-icon user="Alexandr C." role="Администратор" image="photo.jpg"></user-icon>
    </div>

    <div class="row">
      <breadcrumbs-block :parts="breadcrumbs"></breadcrumbs-block>
    </div>

    <div class="tab-buttons">
      <tab-button>Параметры</tab-button>
      <tab-button>Вопросы</tab-button>
      <tab-button>Логика</tab-button>
      <tab-button>Условия</tab-button>
      <tab-button class="active">Респонденты</tab-button>
    </div>

    <div class="tab-view">
      <poll-block></poll-block>
    </div>

  </div>
</template>

<script lang="ts">
  import InputSearch from "@/components/element/InputSearch.vue";
  import UserIcon from "@/components/element/UserIcon.vue";
  import BreadcrumbsBlock from "@/components/element/BreadcrumbsBlock.vue";
  import TabButton from "@/components/element/TabButton.vue";
  import PollBlock from "@/components/poll/PollBlock.vue";
  import {Component, Vue} from 'vue-property-decorator';

  @Component({
    components: {InputSearch, UserIcon, BreadcrumbsBlock, TabButton, PollBlock}
  })
  export default class ContentBlock extends Vue {
    breadcrumbs = ['Опросы', 'Добавить опрос'];
  }
</script>

<style scoped lang="scss">
  @import "../../styles/colors";

  .content-block {
    display: block;
    flex-grow: 1;
    margin-left: 1.5em;
    margin-right: .5em;
    padding-top: 1em;
    padding-bottom: 1em;
  }

  .tab-view {
    border-top: 1px solid $add-color;
    box-shadow: 0 0.5em 0.5em silver;
  }

  .tab-buttons {
    display: flex;
  }

  .row {
    display: flex;
    justify-content: space-between;
    margin-bottom: 1em;
  }
</style>
