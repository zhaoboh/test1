<template>
  <div class="position">
    <span class="iconfont position__icon">&#xe7f1;</span>
    北京理工大学国防科技园2号楼10层
    <span class="iconfont position_notice">&#xe887;</span>
  </div>
  <div class="search">
    <span class="iconfont">&#xe6e1;</span>
    <span class="search__text">山姆会员商店优惠商品</span>
  </div>
  <div class="banner">
    <img
      class="banner__img"
      src="http://www.dell-lee.com/imgs/vue3/banner.jpg"
    />
  </div>
  <div class="icons">
    <div class="icons__item"
    v-for="item in iconList"
    :key="item.desc"
    >
      <img
        class="icons__item__img"
        :src="`http://www.dell-lee.com/imgs/vue3/${item.imgName}.png`"
      />
      <p class="icons__item__desc">{{item.desc}}</p>
    </div>
  </div>
  <div class="gap"></div>
</template>

<script>
export default {
  name: "StaticPart",
  setup() {
    const iconList = [
      { imgName: "红包", desc: "红包套餐" },
      { imgName: "红包", desc: "红包套餐" },
      { imgName: "红包", desc: "红包套餐" },
      { imgName: "红包", desc: "红包套餐" },
      { imgName: "红包", desc: "红包套餐" },
      { imgName: "红包", desc: "红包套餐" },
      { imgName: "红包", desc: "红包套餐" },
      { imgName: "红包", desc: "红包套餐" },
      { imgName: "红包", desc: "红包套餐" },
      { imgName: "红包", desc: "红包套餐" },
    ];
    return { iconList };
  },
};
</script>

<style lang="scss" scoped>
.position {
  position: relative;
  padding: 16px 24px 16px 0;
  line-height: 22px;
  font-size: 16px;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  .position__icon {
    position: relative;
    top: 1px;
    font-size: 20px;
  }
  .position_notice {
    position: absolute;
    right: 0;
    top: 17px;
    font-size: 20px;
  }
}
.search {
  margin-bottom: 12px;
  line-height: 32px;
  background: #f5f5f5;
  color: #b7b7b7;
  border-radius: 16px;
  .iconfont {
    font-size: 16px;
    display: inline-block;
    padding: 0 8px 0 16px;
  }
  &__text {
    display: inline-block;
    font-size: 14px;
  }
}
.banner {
  &__img {
    width: 100%;
  }
}

.icons {
  display: flex;
  flex-wrap: wrap;
  margin-top: 16px;
  &__item {
    width: 20%;
    &__img {
      display: block;
      width: 40px;
      height: 40px;
      margin: 0 auto;
    }
    &__desc {
      margin: 6px 0 16px 0;
      text-align: center;
      color: black;
    }
  }
}
.gap {
  height: 10px;
  background: #f1f1f1;
  margin: 0 -18px;
}
</style>