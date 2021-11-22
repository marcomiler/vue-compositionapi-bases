<template>
  <div class="home">
    <h1>Reactive vs Ref</h1>
    <h3>{{ ironman }}</h3>
    <h3>{{ hulk }}</h3>

    <button @click="changeIronman">Cambiar Ironman</button>
    <button @click="changeHulk">Cambiar Hulk</button>
  </div>
</template>

<script>
import { ref, reactive } from 'vue';
//reactive solo trabaja con objetos y ref; con variables primitivas
export default {
  name: 'Home',

  setup(){
    const ironman = ref({name: 'Tony', age: 50});
    const hulk = reactive({name: 'Bruce', age: 30});

    return {
      ironman,
      hulk,


      changeIronman: () => {
        ironman.value.name = 'Tonny Stark',
        ironman.value.age = 55
      },

      changeHulk: () => {
        hulk.name = 'Bruce Banner',
        hulk.age = 54
      }
    }
  }
}
</script>
