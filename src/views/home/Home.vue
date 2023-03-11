<template>
  <div class="warpper">
    <StaticPart />
    <Nearby />
    <Docker />
  </div>

  <docker />
</template>
<script>
import StaticPart from "./StaticPart.vue";
import Nearby from "./Nearby.vue";
import Docker from "./Docker.vue";
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Home",
  components: { StaticPart, Nearby, Docker },
};
</script>
<style lang="scss" scoped>
.warpper {
  position: absolute;
  left: 0;
  top: 0;
  bottom: 5px;
  right: 0;
  padding: 0 18px;
  overflow-y: auto;
  padding: 0 18px 3px 18px;
}
</style>
