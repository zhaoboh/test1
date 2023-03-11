<template>
  <div class="docker">
    <div
      v-for="(item, index) in dockerList"
      :class="{'docker__item': true, 'docker__item--active': index === currentIndex}"
      :key="item.icon"
    >
      <router-link :to='item.to'>
        <div class="iconfont" v-html="item.icon" />
        <div class="docker__title">{{item.text}}</div>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "Docker",
   props: ['currentIndex'],
  setup() {
    const dockerList = [
      {icon:'&#xe635',text:'首页', to: {name: 'Home'}},
      {icon:'&#xe6af',text:'购物车', to: {name: 'CartList'}},
      {icon:'&#xe7b3',text:'订单', to: {name: 'OrderList'}},
      {icon:'&#xe78b',text:'我的', to: {name: 'Home'}},
    ]
    return { dockerList }
  },
  
};
</script>

<style lang="scss" scoped>
.docker {
  display: flex;
  position: absolute;
  left: 0;
  bottom: 0;
  box-sizing: border-box;
  padding: 0 0.18rem;
  width: 100%;
  height: 0.49rem;
  border-top: 1px solid #f1f1f1;
  background-color: #f1f1f1;
  color: #333;
  &__item {
    flex: 1;
    text-align: center;
    a {
      color: #333;
      text-decoration: none;
    }
    .iconfont {
      font-size: 18px;
      margin: 7px 0 2px 0;
    }
    &--active {
     a {
        color: #1FA4FC;
      }
    }
  }
  &__title {
    font-size: 10px;
    transform: scale(0.5 0.5);
    transform-origin: center top;
  }
}
</style>