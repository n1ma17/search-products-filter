<template>
  <div class="search-body">
    <div v-if="!products.length" class="search-body__first">
      <span>
        for search something, please enter at least 3 characters
      </span>
    </div>
    <div v-else-if="!products.length < 1" class="search-body__empty">
      <ShopEmptyProduct title="محصولی یافت نشد" />
    </div>
    <div v-else class="shop-product__single-product search-body__result">
      <div class="shop-product__single-product__content">
        <div class="w-100">
          <span class="search-body__result--title">نتیجه جستجو:</span>
          <span class="search-body__result--res"
            >{{ products.length }} محصول</span
          >
        </div>
        <div v-for="item in products" :key="item.id" class="mt-3">
          <ShopProductCard
            :id="item.id"
            :item="item.attributes"
            clickable
            :active-id="selectedProduct"
            @clickButton="setProduct(item)"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ShopEmptyProduct from './ShopEmptyProduct.vue'
export default {
  name: 'SearchModalContent',
  components: {
    ShopEmptyProduct
  },
  props: {
    products: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    setProduct(item) {
      console.log(item)
    }
  }
}
</script>

<style lang="scss" scoped>
.search-body {
  display: flex;
  justify-content: center;
  align-items: center;
  &__first {
    padding: 70px 20px;
    gap: 8px;
    align-self: stretch;
    color: #474747;
    text-align: center;
    font-size: 14px;
    font-weight: 400;
    line-height: 160%; /* 22.4px */
  }
  &__empty {
    padding: 128px 20px;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 12px;
    align-self: stretch;
  }
  &__result {
    &--title {
      color: #222;
      text-align: center;
      font-size: 16px;
      font-weight: 600;
      line-height: 160%; /* 25.6px */
    }
    &--res {
      color: #474747;
      text-align: center;
      font-size: 14px;
      font-weight: 400;
      line-height: 160%; /* 22.4px */
    }
  }
}
</style>
