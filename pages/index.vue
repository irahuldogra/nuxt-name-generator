<script setup lang="ts">
enum Gender {
  BOY = 'Boy',
  UNISEX = 'Unisex',
  GIRL = 'Girl',
}
enum Popularity {
  TRENDY = 'Trendy',
  UNIQUE = 'Unique',
}

enum Length {
  LONG = 'Long',
  ALL = 'All',
  SHORT = 'Short',
}

interface OptionsInterface {
  gender: Gender;
  popularity: Popularity;
  length: Length;
}

const options = reactive<OptionsInterface>({
  gender: Gender.BOY,
  popularity: Popularity.UNIQUE,
  length: Length.ALL,
});
</script>

<template>
  <div class="container mx-auto font-sans text-black max-w-4xl text-center">
    <h1>Name Generator</h1>
    <p>Choose your options and click the "Find Names" button below</p>
    <div class="bg-purple-50 rounded-3xl p-3 w-4/5 mx-auto relative">
      <div>
        <h4>1) Choose a gender</h4>
        <div>
          <button
            class="option-left"
            :class="options.gender === Gender.BOY && 'option-active'"
            @click="options.gender = Gender.BOY"
          >
            Boy
          </button>
          <button
            :class="options.gender === Gender.UNISEX && 'option-active'"
            @click="options.gender = Gender.UNISEX"
          >
            Unisex
          </button>
          <button
            class="option-right"
            :class="options.gender === Gender.GIRL && 'option-active'"
            @click="options.gender = Gender.GIRL"
          >
            Girl
          </button>
        </div>
      </div>
      <div>
        <h4>2) Choose the name's popularity</h4>
        <div>
          <button
            class="option-left"
            :class="options.popularity === Popularity.TRENDY && 'option-active'"
            @click="options.popularity = Popularity.TRENDY"
          >
            Trendy
          </button>
          <button
            class="option-right"
            :class="options.popularity === Popularity.UNIQUE && 'option-active'"
            @click="options.popularity = Popularity.UNIQUE"
          >
            Unique
          </button>
        </div>
      </div>
      <div>
        <h4>3) Choose name's length</h4>
        <div>
          <button
            class="option-left"
            :class="options.length === Length.LONG && 'option-active'"
            @click="options.length = Length.LONG"
          >
            Long
          </button>
          <button
            :class="options.length === Length.ALL && 'option-active'"
            @click="options.length = Length.ALL"
          >
            All
          </button>
          <button
            class="option-right"
            :class="options.length === Length.SHORT && 'option-active'"
            @click="options.length = Length.SHORT"
          >
            Short
          </button>
        </div>
      </div>
      <button class="submit-button">Find Names</button>
    </div>
  </div>
</template>
