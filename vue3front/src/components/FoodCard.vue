<template xmlns="http://www.w3.org/1999/html">
  <div class="card-skeleton">
    <div class="card-skeleton__corner-part"></div>
    <div class="card-skeleton__upper-part">
      <div class="card-skeleton__upper-title">Сказочное заморское яство</div>
    </div>
    <div class="card-skeleton__body-part">
      <p class="card-skeleton__food-name">Нямушка</p>
      <p class="card-skeleton__taste">с курой</p>
      <p class="card-skeleton__desc"><span class="card-skeleton__desc_isBold">100</span> порций</p>
      <p class="card-skeleton__desc"><span class="card-skeleton__desc_isBold">5</span> мышей в подарок</p>
      <p class="card-skeleton__desc">заказчик доволен</p>

      <div class="card-skeleton__cat-area">
        <img class="card-skeleton__cat-img" src="../assets/img/Photo.png" alt="">
      </div>

      <div class="card-skeleton__kg-cirlce">
        <div class="card-skeleton__kg-desc">
          <p class="card-skeleton__kg">5</p>
          <p>кг</p>
        </div>
      </div>
    </div>
    <div class="card-skeleton__bottom-title">
      Чего сидишь? Порадуй котэ,&nbsp;<span class="card-skeleton__buy-link">купи</span><span class="card-skeleton__buy-dot">.</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "FoodCard",
  props: {
    params: Object
  },
  data() {
    return {
      
    }
  },
  beforeCreate() {
    console.log(this.params)
  },
  methods: {
    checkParams: function () {

    }
  }
};
</script>

<style lang="scss" scoped>
$background-color: #F2F2F2;
$border-color: #1698D9;

.card-skeleton {
  overflow: hidden;

  width: 100%;
  height: 100%;

  display: grid;

  -ms-grid-rows: 44px 1fr 29px;
  grid-template-rows: 44px 1fr 29px;
  -ms-grid-columns: 44px 1fr;
  grid-template-columns: 44px 1fr;

  flex-direction: column;


  min-height: 509px;
  min-width: 320px;
}

.card-skeleton__upper {
  display: flex;
}

.card-skeleton__corner-part {
  grid-column-start: 1;

  &::after {
    position: absolute;
    content: "";
    width: 86px;
    height: 88px;
    background: $background-color;
    top: 18px;
    left: 3px;
    transform: rotate(45deg);
  }

  &::before {
    position: absolute;
    content: "";
    width:  87.68px;
    height: 87.68px;
    background: none;
    top: -47px;
    left: -55px;
    transform: rotate(45deg);
    border: 4px solid $border-color;
  }
}

.card-skeleton__upper-part {
  background: $background-color;

  border-top: 4px solid $border-color;
  border-right: 4px solid $border-color;
  border-top-right-radius: 12px;

  grid-column-start: 2;
  width: 100%;
}

.card-skeleton__upper-title {
  margin-top: 17px;
  margin-left: 7px;

  color: #666666;
  font-weight: 400;
  font-size: 16px;
}

.card-skeleton__body-part {
  background: $background-color;

  border-left: 4px solid $border-color;
  border-right: 4px solid $border-color;
  border-bottom: 4px solid $border-color;
  border-bottom-left-radius: 12px;
  border-bottom-right-radius: 12px;

  grid-area: 2 / 1 / 2 / 3;

  padding-left: 44px;

  & > p:not(:first-child){
    margin-left: 3px;
  }

  & > p:nth-child(2) {
    margin-bottom: 15px;
  }
}

.card-skeleton__food-name {
  color: #000000;
  font-weight: 700;
  font-size: 48px;
  line-height: 55.73px;
}

.card-skeleton__taste {
  color: #000000;
  font-weight: 700;
  font-size: 24px;
  line-height: 27.87px;

  margin-top: -1px;
}

.card-skeleton__desc {
  color: #666666;
  font-weight: 400;
  font-size: 14px;
  line-height: 16px;
}

.card-skeleton__desc_isBold {
  font-weight: 700;
}

.card-skeleton__kg-cirlce{
  width: 80px;
  height: 80px;

  background: #1698D9;

  -moz-border-radius: 50px;
  -webkit-border-radius: 50px;
  border-radius: 50px;

  position: absolute;
  right: 12px;
  bottom: 12px;

  display: flex;
  flex-direction: column;
  justify-content: center;
}


.card-skeleton__kg-desc {
  width: 100%;
  height: 100%;

  color: #FFFFFF;
  font-weight: 400;
  font-size: 21px;
  line-height: 22px;

  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  text-align: center;

  padding-top: 20px;
  padding-bottom: 8px;
}


.card-skeleton__kg {
  font-size: 42px;
  padding-left: 1px;
}

.card-skeleton__cat-area {
  position: absolute;
  left: 0;
  bottom: 0;

  width: 100%;
  height: 100%;

  border-bottom-left-radius: 7px;
  border-bottom-right-radius: 7px;

  overflow: hidden;
}

.card-skeleton__cat-img {
  position: absolute;
  left: 0;
  bottom: 0;
}

.card-skeleton__bottom-title {
  grid-area: 3 / 1 / 3 / 3;

  color: #FFFFFF;
  font-weight: 400;
  font-size: 13px;
  line-height: 15.09px;

  width: 100%;
  height: 100%;

  display: flex;
  justify-content: center;
  align-items: flex-end;
}

.card-skeleton__buy-link {
  color: #1698D9;
  font-weight: 700;
  text-decoration: underline #1698D9 dashed;
}

.card-skeleton__buy-dot {
  color: #1698D9;
  font-weight: 700;
}

</style>
