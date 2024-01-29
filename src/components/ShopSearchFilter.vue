<template>
  <div class="search-filter">
    <div ref="desktopSearch" class="search-desktop">
      <div class="search-desktop__search-box">
        <CustomTextField
          :value="searchModel"
          has-icon
          clearable
          placeholder="search for products"
          @valueHandler="searchHandler"
        />
      </div>
      <v-expand-transition>
        <div v-if="desktopModal" class="search-desktop__menu">
          <SearchModalContent :products="search.result" />
        </div>
      </v-expand-transition>
    </div>
  </div>
</template>

<script>
import CustomTextField from "./CustomTextField.vue"
import SearchModalContent from "./SearchModalContent.vue"
export default {
  name: "ShopSearchFilter",
  components: {
    SearchModalContent,
    CustomTextField
  },
  props: {
    products: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      desktopModal: false,
      searchModel: "",
      result: [],
      search: {
        term: null,
        text: "",
        modal: false,
        loading: false,
        result: [],
        first: true,
        desktopModal: false
      }
    }
  },
  methods: {
    searchHandler(e) {
      if (e?.length) {
        this.$refs.desktopSearch.classList.add("active")
        this.desktopModal = true
      }else{
        this.$refs.desktopSearch.classList.remove("active")
        this.desktopModal = false
      }
    },
    handleInput(e) {
      if (e.length >= 3) {
        this.search.text = this.search.term
        this.search.result = this.products.filter((product) =>
          product.attributes.name
            .toLowerCase()
            .includes(this.search.term.toLowerCase())
        )
      } else {
        this.search.result = []
      }
    },
    toggleMobileSearchModal() {
      this.search.modal = !this.search.modal
    },
    onSearch() {
      this.search.first = false
      if (this.search.term) {
        const results = this.productList.filter((product) =>
          product.attributes.name.includes(this.search.term)
        )
        this.search.result = results.length > 0 ? results : []
      } else {
        this.search.result = []
        this.search.first = true
      }
    }
  }
}
</script>

<style lang="scss" scoped>

.active {
  z-index: 999;
  border-radius: 8px 8px 0 0;
  background: #fff;
  box-shadow: 0px 15px 8px 0px rgba(0, 0, 0, 0.2);
  border-top: 2px solid #d5d5d529
}
.search-filter {
  width: 100%;
}
.search-desktop {
  display: block;
  position: relative;
  width: 100%;
  height: fit-content;
  padding: 12px 12px 0 12px;
  &__serch-box {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    gap: 12px;
  }
  &__menu {
    position: absolute;
    top: 100%;
    left: 0;
    width: 100%;
    height: 300px;
    background-color: #fff;
    padding: 12px;
    border-radius: 0 0 8px 8px;
    box-shadow: 0px 16px 8px 0px rgba(0, 0, 0, 0.2);
  }
}

.search-box {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  gap: 12px;
  margin-bottom: 24px;
  .v-input {
    height: 36px;
  }
}
</style>
