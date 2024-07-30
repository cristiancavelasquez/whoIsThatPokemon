<template>
  <section
    v-if="isLoading || randomPokemon.id === null"
    class="flex flex-col justify-center items-center w-screen h-screen"
  >
    <h1 class="text-3xl">Please Wait</h1>
    <h3 class="animate-pulse">Loading Pokémons</h3>
    <PokeBall class="w-40 h-40 animate-pulse" />
  </section>

  <section v-else class="flex flex-col justify-center items-center w-screen h-screen">
    <div class="flex justify-center flex-col md:flex-row lg:flex-row items-center">
      <PokeBall class="w-32 h-32" />
      <h1 class="mb-5 mt-5 text-5xl font-black text-amber-500 justify-self-center">
        Who's that Pokemon?
      </h1>
    </div>

    <div class="h-20">
      <button
        v-if="gameStatus !== GameStatus.Playing"
        @click="getNextRound(4)"
        class="bg-blue-500 text-white p-2 rounded-md hover:bg-blue-700 transition-all"
      >
        Play Again?
      </button>
    </div>

    <!-- Pokemon Picture -->
    <PokemonPicture
      :pokemon-id="randomPokemon.id"
      :show-pokemon="gameStatus !== GameStatus.Playing"
    />

    <!-- Pokemon Options -->
    <PokemonOptions
      :options="options"
      :block-selection="gameStatus !== GameStatus.Playing"
      :correct-answer="randomPokemon.id"
      @selected-option="checkAnswer"
    />
  </section>
</template>

<script setup lang="ts">
import PokeBall from '../components/PokeBall.vue';
import PokemonOptions from '../components/PokemonOptions.vue';
import PokemonPicture from '../components/PokemonPicture.vue';
import { usePokemonGame } from '../composables/usePokemonGame';
import { GameStatus } from '../interfaces';

const {
  randomPokemon,
  isLoading,
  gameStatus,
  pokemonOptions: options,
  checkAnswer,
  getNextRound,
} = usePokemonGame();
</script>
