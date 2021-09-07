<template>
  <div class="templates">
    <h1 class="titles__h1">Digito seu peso e altura para calcular o IMC</h1>
    <fieldset>
      <legend>
        <h2 class="titles__h2"> Cálculo do IMC </h2>
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
        <Button class="p-button-success bt" label="Calcular" @click="calculate()" />
        <Button class="p-button-warning bt" label="limpar" @click="limpar()" />
      </div>
    </fieldset>


    <fieldset>
      <legend>
        <h2 class="titles__h2">Resultado </h2>  
      </legend>
      <div class="templates__resultado">
        <p>Seu IMC é: {{ imc }} </p>
        <p>Classificação: {{ classification }} </p>
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
      classification: ''
    };
  },
  methods: {
    calculate: function () {
      this.imc = (this.weight / (this.heigth * this.heigth)).toFixed(2);
      if(this.imc < 18.8) {
        this.classification = 'Magreza';
      } else {
        if(this.imc >= 18.5 && this.imc < 25){
          this.classification = 'Normal';
        } else {
          if(this.imc >= 25 && this.imc < 30){
            this.classification = 'Sobrepeso';
          } else {
            if(this.imc >=30 && this.imc <= 40){
              this.classification = 'Obesidade'
            } else {
              this.classification = 'Obesidade Grave'
            }
          }
        }
      }
      console.log(`Altura: ${this.heigth}`);
      console.log(`Peso: ${this.weight}`);
      console.log(`IMC: ${this.imc}`);
    },
    clear: function() {
      this.heigth = null;
      this.weight = null;
      this.imc = null;
      this.classification = '' 
    }
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

.templates__imc .bt {
  margin-right: 5px;
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

.templates__resultado {
  font-size: 1.2rem;
  font-weight: 700;
}
</style>
