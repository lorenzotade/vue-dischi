<template>
  <main>
    <div class="container-fluid">
      <div class="row justify-content-center">
        <!-- mando la prop genres (array) e ricevo il valore degli emit -->
        <FilterRecord
        :genres="genres"
        @selectGenre="selecting"
        @searchAuthor="searching"
        />
      </div>
        <!-- con un ciclo stampo tanti record quanti elementi sono nell'array -->
        <!-- setto poi la prop record in modo da instaurare una comunicazione con il componente -->
      <div class="row lt-record-container justify-content-center">
        <Record
          v-for="(record, index) in filteredRecords" :key="index"
          :record="record"
        />
      </div>
    </div> 
  </main>
</template>

<script>
// importo il record component e axios dai node_modules
import FilterRecord from '@/components/FilterRecord.vue'
import Record from '@/components/Record.vue'
import axios from 'axios';

export default {
  name: 'Main',
  components: {
    FilterRecord,
    Record
  },
  data() {
    // i data ritornano axios per la chiamata API e un array
    // vuoto dove verranno pushati i record che arrivano
    return {
      axios,
      records: [],
      genres: [],
      optSelect: '1',
      authSearch: ''
    }
  },
  methods: {
    // riceve l'emit dal figlio e associa il valore ad una sua
    // variabile per poter essere utilizzato in questo componente
    selecting(opt) {
      this.optSelect = opt;
    },
    searching(text) {
      this.authSearch = text;
    }, 
  },
  computed: {
    // con questa proprietà computata filtro l'array dei records:
    // se la selezione è neutra (1) viene mostrato tutto l'array;
    // se invece viene selezionata una voce, vengono mostrati tutti
    // i record con quel genere
    /* ritorna anche l'array filtrato in base alla ricerca testuale */
    filteredRecords() {
      if (this.optSelect === '1' && this.authSearch === '') {
        return this.records;
      }
      if (this.optSelect != '1') {
        return this.records.filter(record => record.genre === this.optSelect);
      }

      return this.records.filter(record => record.author.toLowerCase().includes(this.authSearch.toLowerCase()))
    },
  },
  created() {
    // alla creazione dell'istanza Vue viene fatta una chiamata API
    // con metodo GET. I dati che arrivano vengono immagazzinati in records[]
    axios.get('https://flynn.boolean.careers/exercises/api/array/music')
      .then(res => {
        this.records = res.data.response;
        res.data.response.forEach(record => {
          if (!this.genres.includes(record.genre)) {
            this.genres.push(record.genre);
          }
        });
      })
      .catch(err => {
        console.log(err);
      })
  }
}
</script>

<style lang="scss" scoped>
  .lt-record-container {
    padding: 30px 15%;
  }
</style>