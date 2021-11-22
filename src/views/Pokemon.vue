<template lang="">
    <h1 v-if="!pokemon && !errorMessage">Buscando...</h1>
    <h1 v-else-if="errorMessage">{{ errorMessage }}</h1>

    <template v-else>
        <h3>{{ pokemon.name }}</h3>
        <img :src="pokemon.sprites.front_default" :alt="pokemon.name">
        <router-link :to="{ name: 'pokemon-search' }">Volver</router-link>
    </template>

</template>

<script>
import { watch } from 'vue';
import { useRoute, onBeforeRouteLeave } from 'vue-router';
import usePokemon from '@/composables/usePokemon';

export default {
    setup(){

        const route = useRoute();
        console.log(route.params.id);

        const {
            pokemon,
            isLoading,
            errorMessage,
            searchPokemon
        } = usePokemon( route.params.id );

        watch(
            () => route.params.id,
            ( /* value, prevValue */ ) => {
                searchPokemon( route.params.id ); 
                // console.log(value, prevValue);
            }
        );

        //metodo que se ejecuta cuando nos retiramos de la ruta actual  o se ejecuta 
        //onDeactivated
        onBeforeRouteLeave(() => {
            const answer = window.confirm('¿Estás seguro que deseas salir?');
            console.log( answer );
        });


        return {
            pokemon,
            isLoading,
            errorMessage,
            searchPokemon
        }

    }
}
</script>
<style lang="">
    
</style>