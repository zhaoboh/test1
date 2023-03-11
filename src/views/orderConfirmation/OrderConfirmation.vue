<template>
  <div class="wrapper">
    <TopArea />
    <ProductList />
    <Order />
  </div>
</template>

<script>
import Order from './Order.vue'
import TopArea from './TopArea.vue'
import ProductList from './ProductList.vue'

export default {
    name:'OrderConfirmation',
    components: { TopArea, ProductList, Order },
    setup() {
        
    },
}
</script>


<style lang="scss" scoped>
.wrapper {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  background: #000;
  overflow-y: scroll;
}
</style>