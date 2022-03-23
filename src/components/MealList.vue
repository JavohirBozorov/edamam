<template>
  <h1>Edamam</h1>
  <div class="input-group">
    <input
      type="text"
      v-model="newMeal"
      @keyup.prevent.enter="findMeal"
      placeholder="Enter Meal Name..."
    />
  </div>
  <div class="spinner" v-if="spinner">
    <SpinnerComponent />
  </div>
  <div class="meal_card" v-show="showCards > 0" v-if="!spinner">
    <MealCard v-for="(meal, index) in meals" :key="index" :meal="meal" />
  </div>
  <div>
    <h2 v-show="showCards === 0" class="info" v-if="!spinner">
      We can't find "{{ defaultMeal }}"
    </h2>
  </div>
</template>
<script>
import axios from "axios";
import MealCard from "./MealCard.vue";
import SpinnerComponent from "@/components/SpinnerComponent.vue";

export default {
  name: "MealList",
  components: {
    MealCard,
    SpinnerComponent,
  },
  data() {
    return {
      APP_ID: "4b0b39d1",
      API_KEY: "651101c0b56840e5cdbf17d71b562fb8",
      newMeal: "",
      defaultMeal: "kebab",
      meals: [],
      showCards: "",
      spinner: false,
    };
  },
  beforeMounted() {},
  mounted() {
    this.getData();
  },
  methods: {
    async findMeal() {
      this.defaultMeal = this.newMeal;
      console.log(this.defaultMeal);

      this.newMeal = "";
      this.getData();
    },
    async getData() {
      this.spinner = true;
      try {
        const main_link = `https://api.edamam.com/search?app_id=${this.APP_ID}&app_key=${this.API_KEY}&q=${this.defaultMeal}`;
        const res = await axios.get(main_link);

        this.meals = res.data.hits;
        const length = this.meals.length;
        this.showCards = length;
        console.log(res.data);
        // console.log(length);
        // console.log(this.showCards);
      } catch (e) {
        console.error(e);
      } finally {
        this.spinner = false;
      }
    },
  },
};
</script>
<style scoped>
.info {
  text-align: center;
}
.meal_card {
  text-align: center;
}
.input-group {
  display: block;
  text-align: center;
  padding: 1rem;
}
input {
  width: 60%;
  font-size: 20px;
  border-radius: 1rem;
  border-color: #ef9273;
  padding: 0.8rem;
  color: #0d0d0d;
}
input:active,
input:focus {
  outline: none;
}
ul li {
  list-style-type: none;
}
</style>
