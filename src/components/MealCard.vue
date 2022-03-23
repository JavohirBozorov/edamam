<template>
  <!-- full Info -->
  <div class="modal-vue">
    <div class="card">
      <img :src="meal.recipe.image" :alt="meal.recipe.label" />
      <h2>{{ meal.recipe.label }}</h2>
      <h3>Calories: {{ meal.recipe.calories.toFixed(2) }} kkal</h3>
      <h3>Weight: {{ meal.recipe.totalWeight.toFixed() }} g</h3>
      <h3>Sourse: {{ meal.recipe.source }}</h3>
      <h3>Dish Type: {{ meal.recipe.dishType[0] }}</h3>
      <h3>Time: {{ meal.recipe.totalTime }} min</h3>
      <button @click="showModal = true">See Ingredients</button>
    </div>
    <!-- overlay -->
    <div class="overlay" v-if="showModal" @click="showModal = false"></div>
    <!-- modal -->
    <div class="modal" v-if="showModal">
      <h3>Ingridients of "{{ meal.recipe.label }}"</h3>
      <!-- <button class="close" @click="showModal = true">X</button> -->
      <ul
        class="ingredient"
        v-for="(item, index) in meal.recipe.ingredientLines"
        :key="index"
      >
        <li>{{ index + 1 }}. {{ item }}</li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  name: "MealCard",
  data() {
    return {
      showModal: false,
    };
  },
  props: {
    meal: {
      type: [Array, Object],
      require: true,
    },
  },
  methods: {},
};
</script>
<style scoped>
.card {
  background-color: #ef9273;
  margin: 1rem;
  padding: 1rem;
  display: inline-block;
  border-radius: 2rem;
  width: 300px;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 9px 24px;
}
img {
  border-radius: 1rem 1rem 0 0;
}
ul li {
  list-style-type: none;
}
.ingredient {
  position: relative;
  text-align: start;
}
button {
  background-color: #038af9;
  border: none;
  color: #fff;
  font-size: 1rem;
  padding: 0.5rem;
  border-radius: 0.4rem;
}
button:hover {
  cursor: pointer;
}
/* modal */
.modal h3 {
  text-align: start;
  margin-left: 5%;
}
.modal-vue .overlay {
  position: fixed;
  z-index: 1;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.9);
}
.modal-vue .modal {
  position: fixed;
  z-index: 2;
  margin: auto;
  background-color: #fff;
  border-radius: 10px;
}
@media only screen and (min-width: 1200.01px) {
  .modal-vue .modal {
    top: 1rem;
    left: 28rem;
    width: 500px;
  }
}
@media only screen and (max-width: 1200px) {
  .modal-vue .modal {
    top: 1rem;
    left: 23rem;
  }
}
@media only screen and (max-width: 992px) {
  .modal-vue .modal {
    top: 1rem;
    left: 15rem;
  }
}
@media only screen and (max-width: 768px) {
  .modal-vue .modal {
    top: 1rem;
    left: 9rem;
  }
}
@media only screen and (max-width: 576px) {
  .modal-vue .modal {
    top: 1rem;
    left: 1rem;
    padding: 20px 20px;
  }
}
@media only screen and (max-width: 440px) {
  .modal-vue .modal {
    top: 1rem;
    left: 0.5rem;
    width: 85%;
  }
}
@media only screen and (max-width: 360px) {
  .modal-vue .modal {
    top: 1rem;
    left: 2px;
    padding: 0;
    width: 100%;
  }
}
</style>
