<script setup lang="ts">
  import { Gender, Length, Popularity, names } from '@/data';

  interface Payload {
    value: string;
    category: 'length' | 'popularity' | 'gender';
  };

  interface OptionState {
    gender: Gender;
    popularity: Popularity;
    length: Length;
  };

  const options = reactive<OptionState>({
    gender: Gender.GIRL,
    popularity: Popularity.UNIQUE,
    length: Length.SHORT,
  });

  const selectedNames = ref<string[]>([]);

  function computeSelectedNames() {
    selectedNames.value = names
      .filter(name => {
        return name.gender === options.gender &&
          name.popularity === options.popularity;
      })
      .filter(name => {
        if (options.length === Length.ALL) return true;

        return name.length === options.length;
      })
      .map(name => name.name);
  };

  function clickHandler(payload: Payload) {
    //@ts-ignore
    options[payload.category] = payload.value;
  };

  function removeCard(name: string) {
    selectedNames.value = selectedNames.value.filter(n => n !== name);
  };

  const optionsArray = [
    {
      title: '1) Choose gender',
      category: 'gender',
      buttons: [
        Gender.BOY,
        Gender.GIRL,
        Gender.UNISEX
      ],
    },
    {
      title: '2) Choose the name\'s popularity',
      category: 'popularity',
      buttons: [
        Popularity.TRENDY,
        Popularity.UNIQUE
      ],
    },
    {
      title: '3) Choose the name\'s length',
      category: 'length',
      buttons: [
        Length.ALL,
        Length.LONG,
        Length.SHORT
      ],
    }
  ];
</script>

<template>
  <div class="main_container">
    <h1>Baby Name Generator</h1>

    <p>Choose your options and click "Find Name" button below</p>

    <div class="options_container">
      <Option 
        v-for="option in optionsArray"
        :key="option.category"
        :option="option"
        :options="options"
        @click-on-button="clickHandler"
      />

      <button
        class="primary_btn"
        @click="computeSelectedNames"
      >Find Name</button>
    </div>

    <div class="cards_container">
      <CardName 
        v-for="name of selectedNames"
        :key="name"
        :name="name"
        @remove-card="removeCard"
      />
    </div>
  </div>
</template>

<style scoped>
  .main_container {
    font-family: Arial, Helvetica, sans-serif;
    color: rgb(27, 60, 138);
    text-align: center;
    margin: 0px auto;
    max-width: 50rem;
  }

  h1 {
    font-size: 3rem;
  }

  .primary_btn {
    background-color: rgb(249, 87, 89);
    color: white;
    border: none;
    padding: 0.75rem 4rem;
    border-radius: 6.5rem;
    font-size: 1rem;
    cursor: pointer;
    margin-top: 1rem;
  }

  .cards_container {
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
    margin-top: 3rem;
  }
</style>
