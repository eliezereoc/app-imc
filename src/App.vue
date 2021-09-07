<template>
  <!--<div>
     <div class="titles">
      <h1 class="titles__h1">Cálculo do IMC</h1>
      <h2 class="titles__h2">Digito seu peso e altura para calcular o IMC</h2>
    </div>

    <div class="templates">
      <div class="templates__imc">
        <span class="p-float-label">
          <InputText id="input-weight" type="text" v-model="weight" />
          <label for="input-weight">Peso</label>
        </span>
      </div>

      <div class="templates__imc">
        <span class="p-float-label">
          <InputText id="input-weight" type="text" v-model="heigth" />
          <label for="input-weight">Altuara</label>
        </span>
      </div>

      <div class="templates__imc">
        <Button class="bt" label="Calcular" @click="calculate()" />
      </div>
    </div>
  </div> -->
  <div class="templates">
    <h1 class="titles__h1">Cálculo do IMC</h1>
    <fieldset>
      <legend>
        <h2 class="titles__h2">Digito seu peso e altura para calcular o IMC</h2>
      </legend>

      <div class="templates__imc">
        <span class="p-float-label">
          <InputText id="input-weight" type="text" v-model="weight" />
          <label for="input-weight">Peso</label>
        </span>
      </div>

      <div class="templates__imc">
        <span class="p-float-label">
          <InputText id="input-weight" type="text" v-model="heigth" />
          <label for="input-weight">Altura</label>
        </span>
      </div>

      <div class="templates__imc">
        <Button class="bt" label="Calcular" @click="calculate()" />
      </div>
    </fieldset>
  </div>
</template>

<script>
export default {
  data() {
    return {
      heigth: null,
      weight: null,
      imc: null
    };
  },
  methods: {
    calculate: function () {

      this.imc = (this.weight / (this.heigth * this.heigth)).toFixed(2);

      console.log(`Altura: ${this.heigth}`);
      console.log(`Peso: ${this.weight}`);
      console.log(`IMC: ${this.imc}`);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.templates {
  /* display: flex; */
  /* flex-flow: row nowrap; */
  max-width: 1200px;
  margin: 0 auto;
}

.templates__imc {
  margin-top: 2rem;
  padding-left: 1rem;
}

.titles {
  padding-left: 1rem;
}

.titles__h1 {
  font-size: 2rem;
}

.titles__h2 {
  font-size: 1.1rem;
}
</style>
