<script setup lang="ts">
  import { Gender, Length, Popularity } from '../data';

  interface OptionProps {
    option: {
      title: string;
      category: string;
      buttons: Gender[] | Length[] | Popularity[];
    };
    options: {
      length: Length;
      popularity: Popularity;
      gender: Gender;
    };
  };

  const props = defineProps<OptionProps>();
  const emit = defineEmits(['clickOnButton']);
</script>

<template>
  <div class="option_container">
      <h4>{{ option.title }}</h4>

      <button
        v-for="value in option.buttons"
        :key="value"
        :class="options[option.category as keyof typeof options] === value && 'option_active'"
        @click="emit('clickOnButton' ,{
          value,
          category: option.category,
        })"
      >{{ value.toLocaleUpperCase() }}</button>
    </div>
</template>

<style scoped>
.options_container {
    background-color: rgb(244, 187, 222);
    border-radius: 2rem;
    padding: 1rem;
    width: 95%;
    margin: 1rem;
    margin-top: 4rem;
    position: relative;
  }

  .option_container {
    margin-bottom: 2rem;
  }

  .option_container button {
    background: white;
    outline: 0.15rem solid rgb(249, 87, 89);
    border: none;
    padding: 0.75rem;
    width: 12rem;
    font-size: 1rem;
    color: rgb(27, 60, 138);
    cursor: pointer;
    font-weight: 200;
  }

  .option_container button:first-of-type {
    border-top-left-radius: 1rem;
    border-bottom-left-radius: 1rem;
  }

  .option_container button:last-of-type {
    border-top-right-radius: 1rem;
    border-bottom-right-radius: 1rem;
  }

  button.option_active {
    background-color: rgb(249, 87, 89);
    color: white;
  }
</style>