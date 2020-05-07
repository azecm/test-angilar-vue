<template>
  <div class="result-block">
    <section>
      <article>
        <h2>Результат</h2>
        {{viewData}}
      </article>
      <p>Кликните в любом месте для закрытия окна</p>
    </section>
  </div>
</template>

<script lang="ts">

  import {Component, Vue, Prop} from 'vue-property-decorator';
  import {ResultInterface} from "@/components/poll/_common";

  @Component
  export default class ResultBlock extends Vue {
    @Prop()
    data!: ResultInterface;

    get viewData() {
      const res = this.data.items.length ? JSON.stringify(this.data) : 'Нет данных';
      console.log(res);
      if (this.data.items.length) {
        fetch('/api/', {credentials: 'include', method: 'post', body: JSON.stringify(this.data)}).then(() => {
          console.log();
        }).catch(() => {
          console.log();
        });
      }
      return res;
    }
  }
</script>

<style scoped lang="scss">
  .result-block {
    display: flex;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.3);
    align-items: center;
    justify-content: center;
  }

  section {
    text-align: center;
    padding: 1em;
    border-radius: 0.5em;
    background-color: white;
    max-width: 500px;
  }

  article {
    margin-bottom: 1em;
  }

  p {
    color: silver;
  }
</style>
