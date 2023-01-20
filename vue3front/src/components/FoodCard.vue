<template xmlns="http://www.w3.org/1999/html">
  <div class="card-skeleton">
    <div class="card" @mouseenter="isFocus = true" @mouseleave="mouseLeave" @click="isClick = true">
      <div class="card-skeleton__corner-part"
           :class="[isSelect ? 'card-skeleton__corner-part_isSelect' : '',
                    disabled ? 'card-skeleton__corner-part_isDisable' : '']"></div>
      <div class="card-skeleton__upper-part" :class="[isSelect ? 'card-skeleton__upper-part_isSelect' : '',
                                                      disabled ? 'card-skeleton__upper-part_isDisable' : '']">
        <div class="card-skeleton__upper-title" :class="[isSelect && isFocus ? 'card-skeleton__upper-title_isSelect' : '',
                                                         disabled ? 'card-skeleton__upper-title_isDisable' : '']">
          {{ isSelect && isFocus ? "Котэ не одобряет?" : "Сказочное заморское яство" }}
        </div>
      </div>
      <div class="card-skeleton__body-part"  :class="[isSelect ? 'card-skeleton__body-part_isSelect' : '',
                                                      disabled ? 'card-skeleton__body-part_isDisable' : '']">
        <p class="card-skeleton__food-name">Нямушка</p>
        <p class="card-skeleton__taste">{{ labels.taste }}</p>
        <p class="card-skeleton__desc">
          <span class="card-skeleton__desc_isBold">{{ labels.portions }}</span> {{ declension(["порция", "порции", "порций"], labels.portions) }}</p>
        <p class="card-skeleton__desc"><span class="card-skeleton__desc_isBold">{{ labels.mouseAmount === 1 ? '' : labels.mouseAmount }}</span> {{ declension(["мышь", "мыши", "мышей"], labels.mouseAmount) + " в подарок"}}</p>
        <p class="card-skeleton__desc">{{ labels.additionalTitle }}</p>

        <div class="card-skeleton__cat-area">
          <img class="card-skeleton__cat-img" :src="'./img/' + (disabled ? 'cat-disable' : 'cat') + '.png'" alt="">
        </div>

        <div class="card-skeleton__kg-cirlce" :class="[isSelect ? 'card-skeleton__kg-cirlce_isSelect' : '',
                                                       disabled ? 'card-skeleton__kg-cirlce_isDisable' : '']">
          <div class="card-skeleton__kg-desc">
            <p class="card-skeleton__kg">{{ labels.kilo.toString().replaceAll('.', ',') }}</p>
            <p>кг</p>
          </div>
        </div>
      </div>
    </div>
    <div class="card-skeleton__bottom-title" :class="disabled ? 'card-skeleton__bottom-title_isDisable' : ''">
      {{ this.disabled ? "Печалька, " + labels.taste + " закончился." : (this.isSelect ? this.labels.tasteDescripition || "" : "Чего сидишь? Порадуй котэ,&nbsp;") }}
      <span v-show="!isSelect && !disabled" ><span @click="isClick = true; mouseLeave()" class="card-skeleton__buy-link">купи</span>
        <span class="card-skeleton__buy-dot">.</span></span>
    </div>
  </div>
</template>

<script>

export default {
  name: "FoodCard",
  props: {
    labels: Object,
    disabled: Boolean
  },
  data() {
    return {
      isSelect: false,
      isClick: false,
      isFocus: false,
      someData: {
        elem1: "useful information"
      }
    }
  },
  mounted() {
    // this.$emit('test', 'someValue')
  },
  methods: {
    mouseLeave: function () {
      if (this.disabled) return

      if (this.isClick) {
        this.isSelect = !this.isSelect;
        this.$emit('send-data', this.someData)
      }

      this.isClick = false;
      this.isFocus= false;
    },
    checkParams: function () {

    },
    declension: function (forms, val) {
      const cases = [ 2, 0, 1, 1, 1, 2 ];
      return forms[(val % 100 > 4 && val % 100 < 20) ? 2 : cases[(val % 10 < 5) ? val % 10 : 5]];
    }
  }
};
</script>

<style lang="scss" scoped>
$background-color: #F2F2F2;
$border-color: #1698D9;
$select-color: #D91667;
$disable-color: #B3B3B3;

.card-skeleton {
  overflow: hidden;

  width: 100%;
  height: 100%;

  min-height: 509px;
  min-width: 320px;

  display: grid;
  -ms-grid-rows: 1fr 29px;
  grid-template-rows: 1fr 29px;

  cursor: default;
}

.card {
  $table: 44px 1fr;

  width: 100%;
  height: 100%;

  display: grid;
  -ms-grid-rows: $table;
  grid-template-rows: $table;
  -ms-grid-columns: $table;
  grid-template-columns: $table;
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
    border: 5px solid $border-color;
  }
}

.card-skeleton__corner-part_isSelect::before {
  border-color: $select-color;
}

.card-skeleton__corner-part_isDisable::before {
  border-color: $disable-color;
}

.card-skeleton__upper-part {
  background: $background-color;

  border-top: 4px solid $border-color;
  border-right: 4px solid $border-color;
  border-top-right-radius: 12px;

  grid-column-start: 2;
  width: 100%;
}

.card-skeleton__upper-part_isSelect {
  border-color: $select-color;
}

.card-skeleton__upper-part_isDisable {
  border-color: $disable-color;
}

.card-skeleton__upper-title {
  margin-top: 17px;
  margin-left: 7px;

  color: #666666;
  font-weight: 400;
  font-size: 16px;
}

.card-skeleton__upper-title_isSelect {
  color: $select-color;
}

.card-skeleton__upper-title_isDisable {
  color: $disable-color;
  opacity: 0.5;
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

.card-skeleton__body-part_isSelect {
  border-color: $select-color;
}

.card-skeleton__body-part_isDisable {
  border-color: $disable-color;

  & > p {
    color: $disable-color;
    opacity: 0.5;
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

.card-skeleton__kg-cirlce_isSelect {
  background: $select-color;
}

.card-skeleton__kg-cirlce_isDisable {
  background: $disable-color;
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
  pointer-events: none;
  user-select: none;
}

.card-skeleton__cat-img {
  position: absolute;
  left: 0;
  bottom: 0;
}

.card-skeleton__cat-img_isDisable {
  mix-blend-mode: normal;
  opacity: 0.5;
}

.card-skeleton__bottom-title {
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

.card-skeleton__bottom-title_isDisable {
  color: #FFFF66;
}

.card-skeleton__buy-link {
  color: #1698D9;
  font-weight: 700;
  text-decoration: underline #1698D9 dashed;

  cursor: pointer;
}

.card-skeleton__buy-dot {
  color: #1698D9;
  font-weight: 700;
}

</style>
