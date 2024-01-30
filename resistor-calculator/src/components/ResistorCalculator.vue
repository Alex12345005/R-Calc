<template>
    <div class="resistor-calculator">
      <h2>R-Kalkulator</h2>
      <div v-for="(input, index) in inputs" :key="index" class="input-group">
        <input class="input" v-model.number="inputs[index]" type="number" placeholder="Widerstandswert (Ohm)" />
        <button class="button" v-if="inputs.length > 1" @click="removeInput(index)">Löschen</button>
      </div>
      <button class="button" @click="addInput">Weiteren Wert hinzufügen</button>
  
      <div>
        <input type="radio" id="series" value="series" v-model="connectionType" />
        <label for="series">Serienschaltung</label>
        <input type="radio" id="parallel" value="parallel" v-model="connectionType" />
        <label for="parallel">Parallelschaltung</label>
      </div>
  
      <button class="button" @click="calculateTotalResistance">Berechnen</button>
      <p v-if="totalResistance !== null">Gesamtwiderstand: {{ totalResistance }} Ohm</p>
    </div>
  </template>
  
  
  <script>
  export default {
    data() {
      return {
        inputs: [0],
        connectionType: 'series',
        totalResistance: null
      };
    },
    methods: {
      addInput() {
        this.inputs.push(0);
      },
      removeInput(index) {
        if (this.inputs.length > 1) {
          this.inputs.splice(index, 1);
        }
      },
      calculateTotalResistance() {
        if (this.connectionType === 'series') {
          this.totalResistance = this.inputs.reduce((a, b) => a + b, 0);
        } else {
          this.totalResistance = 1 / this.inputs.reduce((a, b) => a + 1 / b, 0);
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .resistor-calculator {
    padding: 20px; 
    max-width: 800px;
    margin: 0 auto;
    margin-top: 100px;
    background: #fff;
    box-shadow: 0 0 10px rgba(0,0,0,0.1); 
  }
  
  .input-group {
    margin-bottom: 10px;
  }
  
  </style>
  
  