<script setup>
import FoodCard from "./components/FoodCard.vue";
</script>

<template>
  <main>
    <div class="title">Ты сегодня покормил кота?</div>
    <div class="food-cards">
      <div class="food-cards__card">
        <FoodCard :params="params1"></FoodCard>
      </div>
      <div class="food-cards__card">
        <FoodCard :params="params2"></FoodCard>
      </div>
      <div class="food-cards__card">
        <FoodCard :params="params3"></FoodCard>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "FoodCard",
  data() {
    return {
      params1: {
        taste: "с фуа-гра",
        portions: 10,
        mouseAmount: 1,
        kilo: 0.5,
        additionalTitle: "заказчик доволен"

      },
      params2: {

      },
      params3: {

      },
    }
  }
};
</script>

<style lang="scss" scoped>
main {
  padding-top: 36px;
}

.title {
  color: #FFFFFF;
  font-family: 'Exo2.0', monospace;
  font-size: 36px;
  line-height: 44px;

  text-align: center;

  height: 44px;
  margin-bottom: 24px;
}

.food-cards {
  display: flex;

  // Первый вариант (тянется расстояние между экраном и карточками)
  justify-content: space-evenly;

  // Второй вариант (по центру с разрывом в мин. 80px между карточками)
  //justify-content: center;
  //column-gap: 80px;
}

.food-cards__card {
  width: 320px;
  height: 509px;
}
</style>
