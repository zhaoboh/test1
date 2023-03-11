<template>
  <div class="order">
    <div class="order__price">实付金额 <b>¥{{calculations.price}}</b></div>
    <div class="order__btn" @click="() => handleShowConfirmChange(true)">提交订单</div>
  </div>
  <div
    class="mask"
    v-show="showConfirm"
    @click="() => handleShowConfirmChange(false)"
  >
    <div class="mask__content" @click.stop>
      <h3 class="mask__content__title">确认要离开收银台？</h3>
      <p class="mask__content__desc">请尽快完成支付，否则将被取消</p>
      <div class="mask__content__btns">
        <div
          class="mask__content__btn mask__content__btn--first"
          @click="() => handleConfirmOrder(true)"
        >取消订单</div>
        <div
          class="mask__content__btn mask__content__btn--last"
          @click="() => handleConfirmOrder(false)"
        >确认支付</div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
import { useRouter, useRoute } from 'vue-router' 
import { useStore } from 'vuex'
import { post } from '../../utils/request'
import { useCommonCartEffect } from '../../effects/cartEffects'

const useMakeOrderEffect = (shopId, shopName, productList, ) => {
    const router = useRouter()
    const store = useStore()

    const handleConfirmOrder = async (isCanceled) => { 
        const products = []
        for(let i in productList.value) {
            const product = productList.value[i]
            products.push({id: product._id, num: product.count})
        }
        try {
            const result = await post('/api/order',{
                shopId,
                shopName: shopName.value,
                isCanceled,
                products
            })
            if (result?.errno === 0) {
                store.commit('clearCartDatall', shopId)
                router.push({ name:'OrderList' })
            }
        }catch(e){

        }
    }
    return { handleConfirmOrder }
}

const useShowMaskEffect = () => {
  const showConfirm = ref(false)
  const handleShowConfirmChange = (status) => {
    showConfirm.value = status
  }
  return { showConfirm, handleShowConfirmChange }
}

export default {
    name:'Order',
    setup() {
        const route = useRoute()
        const shopId = route.params.id
        const { calculations, shopName, productList } = useCommonCartEffect(shopId)
        const { handleConfirmOrder } = useMakeOrderEffect(shopId, shopName, productList, )
        const { showConfirm, handleShowConfirmChange } = useShowMaskEffect()
        return { showConfirm, handleShowConfirmChange, calculations, shopName, productList, handleConfirmOrder }
    }, 
}
</script>


<style lang="scss" scoped>
.order {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  height: .49rem;
  line-height: .49rem;
  background: #fff;
  &__price {
    flex: 1;
    text-indent: .24rem;
    font-size: .14rem;
    color: #333;
  }
  &__btn {
    width: .98rem;
    background: #0091ff;
    color: #fff;
    text-align: center;
    font-size: .14rem;
  }
}
.mask {
  z-index: 1;
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  background: rgba(0, 0, 0, .5);
  &__content {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 3rem;
    height: 1.56rem;
    background: #fff;
    text-align: center;
    border-radius: .04rem;
    &__title {
      margin: .24rem 0 0 0;
      line-height: .26rem;
      font-size: .18rem;
      color: #333;
    }
    &__desc {
      margin: .08rem 0 0 0;
      font-size: .14rem;
      color: #666;
    }
    &__btns {
      display: flex;
      margin: .24rem .58rem;
    }
    &__btn {
      flex: 1;
      width: .8rem;
      line-height: .32rem;
      border-radius: .16rem;
      font-size: .14rem;
      &--first {
        margin-right: .12rem;
        border: .01rem solid #0091ff;
        color: #0091ff;
      }
      &--last {
        margin-left: .12rem;
        background: #0091ff;
        color: #fff;
      }
    }
  }
}
</style>