<template>
  <div class="panel">
      <div class="panel__title">
          <h2>Mesero</h2>
          <h3>{{message}}</h3>
      </div>
      <div class="panel__general">
          <h5>
              Total acumulado:
          </h5>
          <h4>
              {{`$ ${total}`}}
          </h4>
          <h5>
              Cantidad de cargas:
          </h5>
          <h4>
              {{inputs}}
          </h4>
      </div>
      <div class="panel__table">
          <h5>
              Mesa seleccionada:
          </h5>
          <h4>
              {{selectedTable ? selectedTable.name : '???'}}
          </h4>
          <h5>
              Total acomulado:
          </h5>
          <h4>
              {{`$ ${tableTotal}`}}
          </h4>
          <h5>
              Cantidad de cargas:
          </h5>
          <h4>
              {{tableInputs}}
          </h4>
      </div>
      <div class="panel__input">
          <input type="text" placeholder="Importe" v-model="amount"/>
          <button @click="changeVariable"> cambiar Variable </button>
      </div>
  </div>
</template>
<script>
let variable = 13;
export default {
  name: 'Panel',
  props: {
      total: Number,
      inputs: Number,
      selectedTable: String,
      tableInputs: Number,
      tableTotal: Number,
  },
  data() {
      return{
          amount: null,
          message: '',
      }
  },
  methods: {
      saveAmount(){
          this.$emit('amount-saved', this.amount);
          this.amount = '';
      },
      changeVariable(){
        variable = variable + 1;
        console.log(variable);
      }
  },
  watch: {
      total: function(newValue, oldValue){
          this.message = `El importe cambio del valor : ${oldValue} al: ${newValue}`
      }
  }
}
</script>

<style>
.panel{
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  width: 100%;
}

.panel__general, .panel__table{
  min-height: 100px;
  border: 1px solid #ccc;
  width: 95%;
  margin: 10px auto;
}

</style>