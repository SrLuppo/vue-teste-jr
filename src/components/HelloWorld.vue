<template>
  <div class="hello">
    <h2>adsfsadfsad</h2>

    Nome: <input type="text" v-model="nome">
    <br><br>
    Ano de nascimento: <input type="number"  @input="calculateIdade()"  v-model="anoDeNascimento" name="" id="">
    <hr>
    Meu nome é: {{nome}}
    <br>
    Minha Idade é {{idade}}
    <hr>

    <input type="button" value="Fazer requisição" @click="getEspecialidades">
  <hr>
<!-- <p v-for="(especialidade,index) in especialidades" v-bind:key="index" >
  {{especialidade.nome}}
</p> -->
<select  name="" id="" >
  <option v-for="(especialidade,index) in especialidades" v-bind:key="index" :value="especialidade.nome">{{especialidade.nome}}</option>
</select>
<hr>
<select @change="getCidades()" name="Estados" v-model="selectedEstadoId" id="" >
  <option  v-for="(estado,index) in estados" v-bind:key="index" :value="estado.id">{{estado.nome}}</option>
</select>
<select  name="cidades"  id="" >
  <option v-for="(cidade,index) in cidades" v-bind:key="index" :value="cidade.nome">{{cidade.nome}}</option>
</select>


  
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'HelloWorld',
  data() {
  return {
    nome: '',
    idade: '0',
    anoDeNascimento: 0,
    especialidades:  this.getEspecialidades(),
    estados: this.getEstados(),
    cidades:'',
    selectedEstadoId: 1,

  }},
  props: {
    msg: String
  },
  methods: {
    getCidades(){
         axios.get('https://api-teste-front-end-fc.herokuapp.com/cidades',{ 
           params:{ 
             estadoId: this.selectedEstadoId 
             }})
           .then((res)=>{
             this.cidades = res.data
            //  console.log(res.data)
           })
           .catch((error)=>{
             console.log(error)
           })
    },
    getEstados(){
            axios.get('https://api-teste-front-end-fc.herokuapp.com/estados')
           .then((res)=>{
             this.estados = res.data
            //  console.log(res.data)
           })
           .catch((error)=>{
             console.log(error)
           })
    },
    calculateIdade(){
      this.idade = 2022 - this.anoDeNascimento
    },
     getEspecialidades(){
      axios.get('https://api-teste-front-end-fc.herokuapp.com/especialidades')
           .then((res)=>{
             this.especialidades = res.data
            //  console.log(res.data)
           })
           .catch((error)=>{
             console.log(error)
           })
    }
  },
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style  scoped>

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
