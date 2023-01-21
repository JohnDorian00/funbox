<template>
  <main>
    <div class="settings">
      <button class="settings__button" @click="changeAmount(true)">
        Добавить кол-во
      </button>
      <button class="settings__button" @click="changeAmount">
        Убавить кол-во
      </button>
      <button class="settings__button" @click="randLabels = []">
        Очистить
      </button>
    </div>
    <div class="title">Ты сегодня покормил кота?</div>
    <div class="food-cards">
      <div class="food-cards__card">
        <FoodCard :labels="labels[0]" @send-data="catchData"></FoodCard>
      </div>
      <div class="food-cards__card">
        <FoodCard :labels="labels[1]" @send-data="catchData"></FoodCard>
      </div>
      <div class="food-cards__card">
        <FoodCard
          :labels="labels[2]"
          @send-data="catchData"
          :disabled="true"
        ></FoodCard>
      </div>
      <div v-for="i in this.randLabels.length" :key="i">
        <FoodCard
          :labels="randLabels[i - 1]"
          @send-data="catchData"
          :disabled="randLabels[i - 1].disabled"
        ></FoodCard>
      </div>
    </div>
  </main>
</template>

<script>
import FoodCard from "./components/FoodCard.vue";

export default {
  name: "App",
  components: {
    FoodCard,
  },
  data() {
    return {
      labels: [
        {
          taste: "с фуа-гра",
          portions: 10,
          mouseAmount: 1,
          kilo: 0.5,
          tasteDescripition: "Печень утки разварная с артишоками.",
        },
        {
          taste: "с рыбой",
          portions: 40,
          mouseAmount: 2,
          kilo: 2,
          tasteDescripition: "Головы щучьи с чесноком да свежайшая сёмгушка.",
        },
        {
          taste: "с курой",
          portions: 100,
          mouseAmount: 5,
          kilo: 5,
          additionalTitle: "заказчик доволен",
          tasteDescripition: "Филе из цыплят с трюфелями в бульоне.",
        },
      ],
      randLabels: [],
    };
  },
  methods: {
    catchData: function (data) {
      console.log("Receive data - ", data);
    },
    getRandomLabels: function () {
      let randLabels = { ...this.labels[Math.floor(Math.random() * 3)] };
      randLabels.disabled = Math.floor(Math.random() * 2);

      return randLabels;
    },
    changeAmount: function (isInc) {
      if (isInc && typeof isInc === "boolean") {
        this.randLabels.push(this.getRandomLabels());
      } else {
        if (this.randLabels.length > 0) {
          this.randLabels.pop();
        }
      }
    },
  },
};
</script>

<style lang="scss" scoped>
main {
  padding-top: 36px;

  display: flex;
  flex-direction: column;

  height: 100%;
}

.settings {
  position: fixed;
  bottom: 0;
  left: 0;
  z-index: 999999999999;

  opacity: 0.8;

  display: grid;
  grid-template-columns: 1fr 1fr;

  & > button:last-child {
    grid-column: 1 / 3;
  }
}

.title {
  color: #ffffff;
  font-family: "Exo2.0", monospace;
  font-size: 36px;
  line-height: 44px;

  text-align: center;
  margin-bottom: 25px;

  flex: 0 0 1px;
}

.food-cards {
  flex: 1 1 1px;

  display: grid;
  //grid-template-columns: repeat(auto-fill, minmax(360px, 1fr));
  grid-template-columns: 1fr 1fr 1fr;
  align-items: center;

  // Первый вариант (тянется расстояние между экраном и карточками)
  //justify-content: space-evenly;
  //align-items: center;

  // Второй вариант (по центру с разрывом в мин. 80px между карточками)
  //justify-content: center;
  //column-gap: 80px;

  & > div {
    align-self: center;
    justify-self: center;
  }
  row-gap: 50px;
}

.food-cards__card {
  width: 320px;
  height: 509px;
}

/* For 4k View */
@media screen and (min-width: 2048px) {
}

/* For Desktop View */
@media screen and (min-width: 1024px) {
  .food-cards {
    grid-template-columns: 1fr 1fr 1fr;

    & > div:nth-child(3n + 1) {
      grid-column: auto;
    }
  }
}

/* For Tablet View */
@media screen and (min-device-width: 768px) and (max-device-width: 1023px) {
  .food-cards {
    grid-template-columns: 1fr 1fr;

    & > div:nth-child(3n + 1) {
      grid-column: 1 / 3;
    }
  }
}

/* For Mobile Portrait View */
@media screen and (max-device-width: 480px) and (orientation: portrait) {
  .food-cards {
    grid-template-columns: 1fr;
  }
}

/* For Mobile Landscape View */
@media screen and (max-device-height: 480px) and (orientation: landscape) {
  .food-cards {
    grid-template-columns: repeat(auto-fill, minmax(360px, 1fr));

    & > div:nth-child(3n + 1) {
      grid-column: auto;
    }
  }
}
</style>
