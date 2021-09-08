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

    <div class="templates__texto-apoio">
      <h2>Definição do IMC </h2>
      <p>O Índice de Massa Corporal (IMC) é utilizado para medir a relação entre peso e altura em pessoas adultas. 
        O cálculo se dá pela fórmula: IMC = Peso (em Kg) / Altura (em m)².
      </p>
      <p>Em indivíduos adultos com idade maior ou igual a vinte anos e menores que sessenta anos, 
        não são aplicáveis cálculos adicionais para a compreensão dos valores resultantes do cálculo do IMC. 
        Sendo assim, para definir a condição nutricional do indivíduo utiliza-se o valor bruto do IMC apurado pela formula. 
      </p>
      <p>
        A categorização nutricional em pessoas adultas se resulta pelo montante cru obtido no cálculo do IMC. 
        Assim, são definidos três faixas para classificar o estado nutricional do indivíduo. 
      </p>       
      <p> 
        <b>São elas:</b>
        <ul>
          <li> <b>IMC menor que 18,5:</b> adulto a baixo do peso.</li>
          <li> <b>IMC maior ou igual a 18,5 e menor que 25,0:</b> adulto com peso satisfatório (eutrófico).</li>
          <li> <b>IMC maior ou igual a 25,0 e menor que 30,0:</b> adulto com sobrepeso.</li>
          <li> <b>IMC maior ou igual a 30,0:</b> adulto com obesidade.</li>
        </ul>
      </p>
      <p>
        <b><i>Atenção</i></b> <br>
        O cálculo do índice de massa corporal não indica o excesso de gordura corporal, 
        pode ocorrer que o valor está sendo atribuído a massa muscular, o que ocorre com frequência em atletas. 
        Dessa forma, o IMC não deve ser utilizado para avaliar a composição corporal do avaliado. 
      </p>
      <figcaption><b>Fonte:</b> 
        <cite>
          <a href="http://tabnet.datasus.gov.br/cgi-win/SISVAN/CNV/notas_sisvan.html" target="_blank">
          SISVAN - Sistema de Vigilância Alimentar e Nutricional</a>
        </cite>  
      </figcaption>
    </div>
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

      this.imc = (this.weight / (altura * altura)).toFixed(1);
      
      if (this.imc < 18.5) {
        this.classification = "Peso abaixo do indicado";
      } else {
        if (this.imc >= 18.5 && this.imc < 25) {
          this.classification = "Peso satisfatório (eutrófico)";
        } else {
          if (this.imc >= 25 && this.imc < 30) {
            this.classification = "Sobrepeso";
          } else {
            if (this.imc >= 30 ) {
              this.classification = "Obesidade";
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
  padding-bottom: 100px;
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

.templates__texto-apoio {
  font-size: 1.1rem;  
  text-align: justify;
}




@media (max-width: 1024px) {

  .templates {
    display: flex;
    align-items: center;
    flex-flow: column wrap;
    margin-left: 15px;
    margin-right: 15px;
    padding-bottom: 100px;   
  }
  
  #footer {
    flex-flow: column wrap;
  }
  #footer #footer__email-phone {
    text-align: center;
  }
  #footer #footer__copyrights {
    text-align: center;
  }  
}
 



</style>
