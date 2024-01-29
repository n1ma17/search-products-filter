<template>
  <div class="shop-empty">
    <div class="shop-empty__vector">
      <img src="../assets/shop-empty.svg" alt="icon" />
    </div>
    <div class="shop-empty__title">
      {{ title }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'ShopEmptyProduct',
  props: {
    title: {
      type: String,
      default: 'No products found'
    }
  }
}
</script>

<style lang="scss" scoped>
.shop-empty {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-size: 14px;
  font-weight: 500;
  color: #222;
  justify-content: center;
  width: 100%;
  &__vector {
    margin-bottom: 16px;
  }
  &__title {
    color: var(--text-secondary, #474747);
    font-size: 14px;
    font-style: normal;
    font-weight: 500;
    line-height: 160%;
    text-align: center;
  }
}
</style>
