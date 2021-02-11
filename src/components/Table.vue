<template>
  <div 
  :class="['table', isSelected ? 'selected' : '']">
      <h2>{{tableName}}</h2>
      <h2>{{`$ ${tableAmount}`}}</h2>
      <button @click="cleanTable">Limpiar</button>
  </div>
</template>

<script>
export default {
  name: 'Table',
  props: {
    tableName: String,
    tableAmount: Number,
    isSelected: Boolean,
  },
  methods: {
    cleanTable() {
      this.$emit('clean');
    }
  }
}
</script>

<style>

.table{
    height: 200px;
    width: 200px;
    border: 1px solid #ccc;
    text-align: center;
    display: flex;
    flex-direction: column;
    align-content: center;
    cursor: pointer;
}

.selected{
  background: #ddd;
}
</style>