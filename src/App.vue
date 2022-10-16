<script setup>

/* Harris-Benedict Calculator (Total Daily Energy Expenditure) */

import { ref, computed } from "vue";
import IconMale from "./components/icons/male.vue"
import IconFemale from "./components/icons/female.vue"

let sex = ref("M");
let height = ref(150);
let weight = ref(80);
let age = ref(50);
let activityLevel = ref(1.55);
let goal = ref(1);


let baseCalories = computed(() => {
  if (sex.value == "M") {
    return Math.ceil(66.5 + (13.75 * weight.value) + (5.003 * height.value) - (6.75 * age.value));
  } else {
    return Math.ceil(655.1 + (9.563 * weight.value) + (1.85 * height.value) - (4.676 * age.value));
  }
})

let activeCalories = computed(() => Math.ceil((baseCalories.value * activityLevel.value) / 10) * 10)

let loseCalories = computed(() => Math.ceil((activeCalories.value * 0.55) / 10) * 10)

</script>

<template>


  <header>
    <p>Quick and easy calorie calculator to help you figure out how many calories you should consume each day.</p>
    <h1>How Many Calories Do I Need Each Day?</h1>
  </header>

  <main>
    <h2>Calorie Calculator</h2>
    <div class="switch-icon">
      <button :class="{ 'active': sex=='M' }" @click="sex = 'M'">
        <IconMale />
      </button>
      <button :class="{ 'active': sex=='F' }" @click="sex = 'F'">
        <IconFemale />
      </button>
    </div>
    <label for="height">Height
      <input type="number" id="height" v-model="height" />
    </label>
    <label for="weight">Weight
      <input type="number" id="weight" v-model="weight" />
    </label>
    <label for="age">Age
      <input type="number" id="age" v-model="age" />
    </label>

    <label>physical activity level
      <div class="switch">
        <button :class="{ 'active': activityLevel==1.375 }" @click="activityLevel=1.375">Sedentary</button>
        <button :class="{ 'active': activityLevel==1.55 }" @click="activityLevel=1.55">Light</button>
        <button :class="{ 'active': activityLevel==1.725 }" @click="activityLevel=1.725">Moderate</button>
        <button :class="{ 'active': activityLevel==1.9 }" @click="activityLevel=1.9">Active</button>
      </div>
    </label>


    <div class="results">

      <div>
        To maintain weight <span>{{activeCalories}}</span></div>
      <div> To lose weight <span>{{baseCalories}}</span></div>
      <div> To lose weight fast<span>{{loseCalories}}</span>
      </div>
    </div>

  </main> 
  <footer>
    <p>*<sup>1</sup> This calculator is for informational purposes only, and you should consult a healthcare provider
      before making any
      health decisions. The framework is based on population-level data. This
      means using the equation to assess individuals should be used with caution. There are many additional factors
      that
      contribute to a person's resting metabolic rate, including medications, lean body mass, and genetics.
    </p>
    <p><strong>&copy; NO copyright. Please feel free to use the code and contact me for questions/ideas</strong><br />
    <a href="mailto:nadezda@gurska.dev">nadezda@gurska.dev</a></p>
  </footer>

</template>

<style lang="scss">
@use './assets/scss/app.scss';
</style>
