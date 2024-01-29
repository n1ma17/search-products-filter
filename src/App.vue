<template>
  <v-app>
    <v-app-bar
      app
      color="grey lighten-4"
      density="compact"
      height="auto"
    >
      <div class="header-search">
        <div class="header-search__content">
          <ShopSearchFilter :products="products" />
        </div>
      </div>
    </v-app-bar>

    <v-main>
      <HelloWorld/>
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import ShopSearchFilter from "./components/ShopSearchFilter.vue"

export default {
  name: 'App',

  components: {
    HelloWorld,
    ShopSearchFilter
  },

  data: () => ({
    //
  }),
};
</script>
<style lang="scss" scoped>
.header-search {
  width: 100%;
  display: flex;
  justify-content: center;
  &__content {
    width: 100%;
    max-width: 500px;
  }
}
</style>