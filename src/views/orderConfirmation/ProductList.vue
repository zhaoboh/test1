<template>
<div class="products">
  <div class="products__title">
    {{shopName}}
  </div>
  <div class="products__wrapper">
    <div class="products__list">
      <div
        v-for="item in productList"
        :key="item._id"
        class="products__item"
      >
        <img class="products__item__img" :src="item.imgUrl" />
        <div class="products__item__detail">
          <h4 class="products__item__title">{{item.name}}</h4>
          <p class="products__item__price">
            <span>
              <span class="products__item__yen">&yen; </span>
              {{item.price}} x {{item.count}}
            </span>
            <span class="products__item__total">
              <span class="products__item__yen">&yen; </span>
              {{(item.price * item.count).toFixed(2)}}
            </span>
          </p>
        </div>
      </div>
    </div>
  </div>
</div>
</template>


<script>
import { useRoute } from 'vue-router'
import { useCommonCartEffect } from '../../effects/cartEffects' 

export default {
    name:'ProductList',
    setup() {
        const route = useRoute()
        const shopId = route.params.shopId
        const { shopName, productList } = useCommonCartEffect(shopId)
        return { shopName, productList }
    },
}
</script>


<style lang="scss" scoped>
.products {
  margin: .16rem .18rem .1rem .18rem;
  background: #fff;
  &__title {
    padding: .16rem;
    font-size: .16rem;
    color: #333;
  }
  &__wrapper {
    overflow-y: scroll;
    margin: 0 .18rem;
    position: absolute;
    left: 0;
    right: 0;
    bottom: .6rem;
    top: 2.6rem;
  }
  &__list {
    background: #fff;
  }
  &__item {
    position: relative;
    display: flex;
    padding: 0 .16rem 0.16rem .16rem;
    &__img {
      width: .46rem;
      height: .46rem;
      margin-right: .16rem;
    }
    &__detail {
      flex: 1;
    }
    &__title {
      margin: 0;
      line-height: .2rem;
      font-size: .14rem;
      color: #333;
    }
    &__price {
      display: flex;
      margin: .06rem 0 0 0;
      line-height: .2rem;
      font-size: .14rem;
      color: #e93b3b;
    }
    &__total {
      flex: 1;
      text-align: right;
      color: #000;
    }
    &__yen {
      font-size: .12rem;
    }
  }
}
</style>