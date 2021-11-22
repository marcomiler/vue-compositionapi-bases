<template lang="">
    <h1>Buscar Pokemon: {{ pokemonId }}</h1>
    <form @submit.prevent="onSubmit">
        <input 
            type="number"
            placeholder="Número del pokemón"
            v-model="pokemonId"
            ref="txtSearchId"
        >
    </form>
    <br>
    <span>Presione enter para buscar</span>
</template>

<script>
import { ref, onActivated } from 'vue'
import { useRouter } from 'vue-router';

export default {
    name: 'SearchPokemon',
    setup(){

        const router = useRouter();

        const pokemonId = ref( 1 );
        const txtSearchId = ref();

        //usaremos onActivated ya que estamos trabajando con keep alive y el componente
        //no se destruye, sino se desmonta. de caso contrario trabajariamos con onMounted
        onActivated(() => {
            txtSearchId.value.select();//o focus
        })
        
        return {
            pokemonId,
            txtSearchId,

            onSubmit: () => {
                //console.log('Pokemon a buscar: ', pokemonId.value);
                router.push({ name: 'pokemon-id', params: { id: pokemonId.value } })
            }
        }

    }
}
</script>
<style lang="">
    
</style>