<template>
  <!-- metto stile al componente record con bootstrap e grazie alla prop stampo nel componente gli elementi che voglio dai record oggetto presenti nell'array in main component -->
  <div class="lt-record-col col-sm-4 col-lg-2 ms-3">
    <img :src="record.poster" :alt="record.title">
    <h2>{{ record.title }}</h2>
    <p>{{ record.author }}</p>
    <p class="year">{{ record.year }}</p>
  </div>
</template>

<script>
export default {
  name: 'Record',
  props: {
    record: Object
  }
}
</script>

<style lang="scss" scoped>
  @import '../assets/style/vars.scss';
  @import '../assets/style/general.scss';

  .lt-record-col {
    min-height: 190px;
    background-color: $header-color;
    margin-bottom: 10px;
    padding: 15px;
    text-align: center;
    &:hover {
      transform: scale(1.03);
    }
    img {
      max-width: 100%;
      margin-bottom: 20px;
    }
  }
</style>