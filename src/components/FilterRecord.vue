<template>
  <section>
    <!-- con il v-model prendo il value dell'option selezionata e al cambiare della selezione (change) viene chiamata la funzione per emettere il dato (value) -->
    <select 
      class="form-select" 
      aria-label="Genre selection"
      v-model="selectedValue"
      @change="filterSelection()"
    >
      <!-- ricevo la prop generes (array) e con i valori in essa contenuti stampo la lista di opzioni della select -->
      <option selected value="1">Click to select a genre</option>
      <option
        v-for="(genre, index) in genres" :key="index"
        :value="genre">{{ genre }}
      </option>
    </select>

    <!-- con il v-model prendo il valore dell'input e al digitare (keyup) viene chiamata la funzione per emettere il dato -->
    <input 
      type="text" 
      placeholder="Search for author"
      class="form-control"
      v-model="authorSearch"
      @keyup="filterAuthor()"
    >

  </section>
</template>

<script>

export default {

  name: 'FilterRecord',
  props: {
    genres: Array
  },
  data() {
    return {
      selectedValue: '1',
      authorSearch: ''
    }
  },
  methods: {
    // trasmetto il value della selezione
    filterSelection() {
      this.$emit('selectGenre', this.selectedValue);
    },
    // trasmetto il valore dell'input
    filterAuthor() {
      this.$emit('searchAuthor', this.authorSearch);
    }
  }
}
</script>

<style lang="scss" scoped>
  @import '../assets/style/vars.scss';

  section {
    padding: 0;
    select {
      background-color: $header-color;
      border: 0;
      border-radius: 0;
      outline: none;
      color: #FFF;
      text-transform: uppercase;
      font-size: 1rem;
      font-weight: 500;
    }
    input {
      background-color: $header-color;
      border: 0;
      border-radius: 0;
      outline: none;
      &::placeholder {
        color: #FFF;
      }
    }
  }

</style>