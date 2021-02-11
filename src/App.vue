<template>
  <div class="app">
    <div class="app__panel">
      <panel
      :total="totalAmount"
      :inputs="totalInputs"
      :selectedTable="selectedTable"
      :tableInputs="selectedTable ? selectedTable.inputs.length : '????'"
      :tableTotal="tableAmount(selectedTable)" 
      @amount-saved="(event) => saveTableAmount(event)"/>
    </div>
    <div class="app__table">
      <m-table v-for="(table, index) in tables" :key="`table-${index}`"
      :tableName="table.name"
      :tableAmount="tableAmount(table)"
      :isSelected="isSelectedTable(index)"
      @click="selectTable(index)"
      @clean="cleanTableInputs(index)"
      />
    </div>
  </div>
</template>

<script>
import Panel from './components/Panel';
import MTable from './components/Table';

export default {
  name: "App",

  components: {
    Panel,
    MTable,
  },
  methods:{
    saveTableAmount(amount){
      const intAmount = parseInt(amount);
      const input = {amount: intAmount}
      this.selectedTable.inputs.push(input);
    },
    tableAmount(table){
      let result = 0;
    if(table){
      table.inputs.forEach(input => {
        result  = result + input.amount;
      })
    }
      return result;
    },
    selectTable(idx){
      this.selectedTable = this.tables[idx];
    },
 
    isSelectedTable(idx){
      const selectedTableIndex = this.tables.indexOf(this.selectedTable);
      return idx === selectedTableIndex;
    },
    cleanTableInputs(idx) {
      this.ganancia += this.tableAmount(this.tables[idx]);
      this.tables[idx].inputs = [];
    }
  },
  computed: {
    totalAmount(){
      let result = 0;
      this.tables.forEach(table => {
        result = result + this.tableAmount(table)
      })

      return result + this.ganancia;
    },
      totalInputs(){
      let result = 0;

      this.tables.forEach(table => {
      result = result + table.inputs.length;
      })
      return result;
    },
  },

  data(){
    return{
      ganancia: 0, 
      selectedTable: null,
      tables: [
        {
          name:'Mesa 1',
          inputs: [],
        },
        {
          name:'Mesa 2',
          inputs: [],
        },
        {
          name:'Mesa 3',
          inputs: [],
        },
        {
          name:'Mesa 4',
          inputs: [],
        },
        {
          name:'Mesa 5',
          inputs: [],
        },
        {
          name:'Mesa 6',
          inputs: [],
        },
        {
          name:'Mesa 7',
          inputs: [],
        },
        {
          name:'Mesa 8',
          inputs: [],
        },
        {
          name:'Mesa 9',
          inputs: [],
        },
      ]
    }
  }
};
</script>

<style>
body {
  margin: 0;
}

.app{
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  display: flex;
  width: 100%;
  height: auto;
}

.app__table{
  flex: 9 0 0;
  display: flex;
  height: 100vh;
  padding: 20px 100px;
  flex-wrap: wrap;
  justify-content: space-around;
}

.app__panel{
  flex: 3 0 0;
  display: flex;
  height: 100vh;
  border: 1px solid #ccc;
}

</style>
