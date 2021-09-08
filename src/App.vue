<template>
  <div class="templates">
    <h1 class="titles__h1">Digito seu peso e altura para calcular o IMC</h1>
    <fieldset>
      <legend>
        <h2 class="titles__h2">Cálculo do IMC</h2>
      </legend>

      <div class="templates__imc">
        <span class="p-float-label">
          <InputText id="input-weight" type="text" v-model="weight" :disabled="imc"/>
          <label for="input-weight">Peso</label>
        </span>
      </div>

      <div class="templates__imc">
        <span class="p-float-label">
          <InputText id="input-weight" type="text" v-model="heigth" :disabled="imc" pattern="^\d{1,7}(,\d{1,3})?$"/>
          <label for="input-weight">Altura</label>
        </span>
      </div>

      <div v-if="!imc" class="templates__imc">
        <Button class="p-button-success bt" label="Calcular" @click="calculate"  :disabled="!weight"/>
        <Button class="p-button-warning bt" label="limpar" @click="clear" :disabled="!weight"/>
      </div>
    </fieldset>

    <fieldset>
      <legend>
        <h2 class="titles__h2">Resultado</h2>
      </legend>
      <div v-if="imc" class="templates__resultado">
        <p>Seu IMC é: {{ imc }}</p>
        <p>Classificação: {{ classification }}</p>
      </div>
      <div v-else class="templates__resultado">
        <p>Digito seu peso e altura e clique no botão calcular.</p>
      </div>
      <div v-if="imc">
        <Button class="p-button-success bt" label="Novo Calculo" @click="clear" />         
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
      imc: null,
      classification: '',
    };
  },
  methods: {
    calculate: function () {
      let altura = this.heigth.replace(',','.');

      this.imc = (this.weight / (altura * altura)).toFixed(2);
      
      if (this.imc < 18.8) {
        this.classification = "Magreza";
      } else {
        if (this.imc >= 18.5 && this.imc < 25) {
          this.classification = "Normal";
        } else {
          if (this.imc >= 25 && this.imc < 30) {
            this.classification = "Sobrepeso";
          } else {
            if (this.imc >= 30 && this.imc <= 40) {
              this.classification = "Obesidade";
            } else {
              this.classification = "Obesidade Grave";
            }
          }
        }
      }
    },
    clear: function () {
      this.heigth = null;
      this.weight = null;
      this.imc = null;
      this.classification = "";
    } 
  }
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

.templates__imc .bt {
  margin-right: 5px;
}

.titles {
  padding-left: 1rem;
}

.titles__h1 {
  font-size: 2rem;
  text-align: center;
}

.titles__h2 {
  font-size: 1.1rem;
}

.templates__resultado {
  font-size: 1.2rem;
  font-weight: 700;
}
</style>
