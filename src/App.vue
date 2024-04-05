<!--
This example demonstrates handling user input with the v-on directive.
-->

<script setup>


import { ref } from 'vue';
import DatePicker from 'vue3-datepicker';
import { fr } from 'date-fns/locale/fr';

import Livre from './components/Livre.vue'

const message = ref('Hello World!');
const estActif = ref(false);
const maListe = ['Janvier','Février','Mars','Avril','Mai','Juin','Juillet','Août','Septembre','Octobre','Novembre','Décembre'];
const multiSelected=ref([]);

const items = [
  { label: 'Option 1', value: 'option1', checked: false },
  { label: 'Option 2', value: 'option2', checked: false },
  { label: 'Option 3', value: 'option3', checked: false }
];

const listeLivres = ref([
  { id: 0, titre: 'Le Fléau' ,auteur : 'Stephen King', dateParution : '15/05/1986' },
  { id: 1, titre: 'Shinning' ,auteur : 'Stephen King', dateParution : '31/12/1981' },
  { id: 2, titre: 'Cujo' ,auteur : 'Stephen King', dateParution : '08/09/1979' }
])

const selectedDate = ref(new Date());

</script>

<template>
<div class="maCase" :class="{ actif: estActif }"  @mouseover="estActif=true" @mouseleave="estActif=false">

  {{ message }}
</div>
<br/>

<ul>
    <li v-for="item of maListe">{{ item }}</li>
</ul>

<br/>
<h2>Multi Select</h2>
  <select v-model="multiSelected" multiple style="width:100px">
    <option v-for="(item, index) in items" :key="index" :value="item.value">
        {{ item.label }}
        
      </option>
  </select>
  <span>Selected: {{ multiSelected }}</span>

  <div>
    <DatePicker v-model="selectedDate" :locale="fr" />
    <p>Date Sélectionnée : {{ selectedDate }}</p>
  </div>

  <ol>
    <!--
      We are providing each todo-item with the todo object
      it's representing, so that its content can be dynamic.
      We also need to provide each component with a "key",
      which is explained in the guide section on v-for.
    -->
    <Livre
      v-for="item in listeLivres"
      :livre="item"
      :key="item.id"
    ></Livre>
  </ol>

</template>

<style>
.maCase {
  padding: 50px;
  background-color: #55cc55;
  border-radius: 10px;
  border: 1px solid #000000;
}
.actif {
  font-weight: bold;
  border:3px solid #000000;
}

</style>