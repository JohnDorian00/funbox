<template>
  <main>
    <div class="title">Ты сегодня покормил кота?</div>
    <div class="food-cards">
      <div class="food-cards__card">
        <FoodCard :labels="labels1" @send-data="catchData"></FoodCard>
      </div>
      <div class="food-cards__card">
        <FoodCard :labels="labels2" @send-data="catchData"></FoodCard>
      </div>
      <div class="food-cards__card">
        <FoodCard :labels="labels3" @send-data="catchData" :disabled="true"></FoodCard>
      </div>
    </div>
  </main>
</template>

<script>
import FoodCard from "./components/FoodCard.vue";

export default {
  name: "App",
  components: {
    FoodCard
  },
  data() {
    return {
      labels1: {
        taste: "с фуа-гра",
        portions: 10,
        mouseAmount: 1,
        kilo: 0.5,
        tasteDescripition: "Печень утки разварная с артишоками."
      },
      labels2: {
        taste: "с рыбой",
        portions: 40,
        mouseAmount: 2,
        kilo: 2,
        tasteDescripition: "Головы щучьи с чесноком да свежайшая сёмгушка."
      },
      labels3: {
        taste: "с курой",
        portions: 100,
        mouseAmount: 5,
        kilo: 5,
        additionalTitle: "заказчик доволен",
        tasteDescripition: "Филе из цыплят с трюфелями в бульоне."
      },
    }
  },
  methods: {
    catchData: function (data) {
      console.log("Receive data - ", data)
    },
  }
};
</script>

<style lang="scss" scoped>
main {
  padding-top: 36px;

  display: flex;
  flex-direction: column;
}

.title {
  color: #FFFFFF;
  font-family: 'Exo2.0', monospace;
  font-size: 36px;
  line-height: 44px;

  text-align: center;
  margin-bottom: 25px;

  flex: 0 0 1px;
}

.food-cards {
  width: 100%;
  height: 100%;

  flex: 1 1 1px;

  display: flex;

  // Первый вариант (тянется расстояние между экраном и карточками)
  justify-content: space-evenly;
  align-items: center;

  // Второй вариант (по центру с разрывом в мин. 80px между карточками)
  //justify-content: center;
  //column-gap: 80px;


  row-gap: 50px;
  padding-bottom: 50px;
}

.food-cards__card {
  width: 320px;
  height: 509px;
}

/* For Desktop View */
@media screen and (min-width: 1024px) {
}

/* For Tablet View */
@media screen and (min-device-width: 768px)
and (max-device-width: 1024px) {

}

/* For Mobile Portrait View */
@media screen and (max-device-width: 480px)
and (orientation: portrait) {
  .food-cards {
    flex-direction: column;
    align-items: center;
  }
}
</style>
