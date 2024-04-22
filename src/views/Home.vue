<script setup>
import { reactive, ref } from 'vue';
import Search from '@/components/icons/Search.vue';
import Location from '@/components/icons/Location.vue';
import ClimaItem from '@/components/ClimaItem.vue';
import Water from '@/components/icons/Water.vue';
import Wind from '@/components/icons/Wind.vue';

const apiChave = ""

const dados = reactive({
  cidade: '',
  pais: '',
  temperatura: '',
  descricao: '',
  descricaoIcon: '',
  umidade: '',
  ventoVel: ''
} );

const carregando = ref(false);
const exibeResultado = ref(false);
const inputCidade = ref("")
const errorCidade = ref("");
const exibeCidade = ref(true);

async function consultaDadosApi(cidade) {
  const apiClimaURL = `https://api.openweathermap.org/data/2.5/weather?q=${cidade}&units=metric&appid=${apiChave}&lang=pt_br`
  
  const req = await fetch(apiClimaURL);
  const data = await req.json();

  return data;
};

async function pesquisar() {
   carregando.value = true;
   errorCidade.value = ''; 
   exibeResultado.value = false;
   
   if (inputCidade == null || inputCidade.value == '') {
    errorCidade.value = 'Digite o nome de uma cidade.'
    carregando.value = false;
    return
   };
   
   const dadosCidade = await consultaDadosApi(inputCidade.value);

   if (dadosCidade.message == 'city not found') {
    errorCidade.value = 'Não foi possível encontrar o clima de uma cidade com este nome.'
    carregando.value = false;
    return
   };
   
   dados.cidade = dadosCidade.name
   dados.temperatura = parseInt(dadosCidade.main.temp);
   dados.descricao = dadosCidade.weather[0].description;
   dados.descricaoIcon = ("src", `http://openweathermap.org/img/wn/${dadosCidade.weather[0].icon}.png`);
   dados.pais = `https://flagsapi.com/${dadosCidade.sys.country}/flat/64.png`
   dados.umidade = `${dadosCidade.main.humidity}%`
   dados.ventoVel = `${dadosCidade.wind.speed}km/h`;

   exibeCidade.value = false;
   exibeResultado.value = true;
   carregando.value = false;

};

async function selecionaCidade(cidade) {
  exibeCidade.value = true;
  inputCidade.value = cidade;
  exibeCidade.value = false;

 pesquisar();
};

</script>

<template>
  <div class="h-screen w-screen flex items-center justify-center bg-gray-100">

    <div class="bg-blue-600 w-72 shadow-md rounded-md p-6 space-y-4 text-center">
      <div>
        <h3 class="text-white text-base font-bold">Confira o clima de uma cidade:</h3>
      </div>
      <div class="flex gap-2 ">
        <input v-model="inputCidade" @keydown.enter="pesquisar" type="text" placeholder="Digite uma cidade"
          class=" focus:outline-none w-full border border-gray-400 rounded placeholder:text-gray-300 px-2 text-base">
        <button @click="pesquisar" class="bg-blue-300 rounded p-1 hover:bg-blue-200">
          <Search/>
        </button> 
      </div>

      <div v-if="carregando" class="animate-spin inline-block size-6 border-[3px] border-current border-t-transparent text-white rounded-full " role="status" aria-label="loading">   
        <span class="sr-only"></span> 
      </div>
      <p v-if="errorCidade" class="text-sm text-gray-200">{{ errorCidade }}</p> 

      <div v-if="exibeCidade" class="gap-4 grid grid-cols-2 border-t pt-5 px-4">
        <button @click="selecionaCidade('maringa')" class="bg-blue-300 rounded-full text-xs text-white hover:bg-blue-200 p-1">Maringá</button>
        <button @click="selecionaCidade('curitiba')" class="bg-blue-300 rounded-full text-xs text-white hover:bg-blue-200 p-1">Curitiba</button>
        <button @click="selecionaCidade('rio de janeiro')" class="bg-blue-300 rounded-full text-xs text-white hover:bg-blue-200 p-1">Rio de Janeiro</button>
        <button @click="selecionaCidade('são Paulo')" class="bg-blue-300 rounded-full text-xs text-white hover:bg-blue-200 p-1">São Paulo</button>
        <button @click="selecionaCidade('brasilia')" class="bg-blue-300 rounded-full text-xs text-white hover:bg-blue-200 p-1">Brasília</button>
        <button @click="selecionaCidade('porto alegre')" class="bg-blue-300 rounded-full text-xs text-white hover:bg-blue-200 p-1">Porto alegre</button>
        <button @click="selecionaCidade('florianopolis')" class="bg-blue-300 rounded-full text-xs text-white hover:bg-blue-200 p-1">Florianopolis</button>
        <button @click="selecionaCidade('fortaleza')" class="bg-blue-300 rounded-full text-xs text-white hover:bg-blue-200 p-1">Fortaleza</button>
      </div>

      <div v-if="exibeResultado" class="text-white space-y-2">
        <div class="flex justify-center items-center gap-1 border-t pt-5 mt-5">
          <Location/>
          <h2 class="font-bold flex capitalize">{{dados.cidade}}</h2>
          <img :src="dados.pais" alt="Bandeira do país" class="h-5">
        </div>
        <p class="text-sm"><span>{{dados.temperatura}}</span> &deg;C</p>

        <div class="flex justify-center items-center">
          <p class="text-sm font-bold capitalize">{{dados.descricao}}</p>
          <img :src="dados.descricaoIcon" alt="Condições do tempo" class="h-10">
        </div>

        <div class="flex justify-center">
          <ClimaItem class="border-r pr-2 w-1/2" :text="dados.umidade" :icon="Water"/>
          <ClimaItem class="pl-2 w-1/2" :text="dados.ventoVel" :icon="Wind"/>
        </div>
      </div>
    </div>
  </div>
</template>
