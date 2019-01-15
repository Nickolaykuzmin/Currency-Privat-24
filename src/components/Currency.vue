<template lang="html">
  <section class="currency">
    <table class="table-responsive table table-bordered table-hover">
      <thead>
        <tr>
          <th class="text-center" scope="col">Код Валюты</th>
          <th class="text-center" scope="col">Курс покупки</th>
          <th  class="text-center" scope="col">Курс продажи</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(currency, index) in data" :key="index">
          <td>{{currency.ccy}}</td>
          <td>{{currency.buy | aroundCurr}}</td>
          <td>{{currency.sale | aroundCurr}}</td>
        </tr>
      </tbody>
    </table>  
  </section>
</template>

<script lang="js">
  export default  {
    name: 'Currency',
    props: ['currencyId'],
    filters: {
      aroundCurr(val) {
        if (val) {
          return Math.ceil(val * 100) / 100;
        }
      }
    },
    mounted() {
      this.axios.get(`https://api.privatbank.ua/p24api/pubinfo?json&exchange&coursid=5`)
        .then(response => {
          this.data = response.data
        })
    },
    data() {
      return {
        data: []
      }
    },
    methods: {

    },
    computed: {

    }
}
</script>

<style scoped>
</style>
