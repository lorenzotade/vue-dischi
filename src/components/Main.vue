<template>
  <main>
    <div class="container-fluid">
      <div class="row justify-content-center">
        <!-- con un ciclo stampo tanti record quanti elementi sono nell'array -->
        <!-- setto poi la prop record in modo da instaurare una comunicazione con il componente -->
        <Record
        v-for="(record, index) in records" :key="index"
        :record="record"
      />
      </div>
    </div> 
  </main>
</template>

<script>
// importo il record component e axios dai node_modules
import Record from '@/components/Record.vue'
import axios from 'axios';

export default {
  name: 'Main',
  components: {
    Record
  },
  data() {
    // i data ritornano axios per la chiamata API e un array
    // vuoto dove verranno pushati i record che arrivano
    return {
      axios,
      records: []
    }
  },
  created() {
    // alla creazione dell'istanza Vue viene fatta una chiamata API
    // con metodo GET. I dati che arrivano vengono immagazzinati in records[]
    axios.get('https://flynn.boolean.careers/exercises/api/array/music')
      .then(res => {
        this.records = res.data.response;
        console.log(this.records);
      })
      .catch(err => {
        console.log(err);
      })
  }
}
</script>

<style lang="scss" scoped>
</style>