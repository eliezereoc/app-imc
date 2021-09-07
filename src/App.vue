<template>
  <div>
    <h1>Cálculo do IMC</h1>
    <h2>Digito seu peso e altura para calcular o IMC</h2>

    <span class="p-float-label">
      <label for="input-weight">Peso</label>
      <InputText id="input-weight" type="text" v-model="weight" />
    </span>

    <span class="p-float-label">
      <label for="input-weight">Altuara</label>
      <InputText id="input-weight" type="text" v-model="weight" />
    </span>

    <Button class="bt" label="Calcular"/>
  </div>
</template>


<script>
export default {
   data() {
    return {
      heigth: null,
      weight: null
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


</style>
