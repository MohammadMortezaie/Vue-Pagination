<template>
  <RentraxPaginator
    :ipp="ipp"
    :productsCount="100"
    :numberCountFirstAndEnd="2"
    :numberShowAll="7"
    :paginationShowCount="13"
    @change-page="(x)=> newPage(x)"
  />
  <RentraxIpp 
  @change-ipp="(x)=> newIpp(x)"
  />
</template>

<script>
import RentraxPaginator from "./components/RentraxPaginator.vue";
import RentraxIpp from "./components/RentraxIpp.vue";

export default {
  data() {
    return {
      ipp:1
    }
  },
  name: "App",
  components: {
    RentraxPaginator,
    RentraxIpp
  },
  methods: {
    newPage(newPage){
      this.page=newPage;
      console.log(newPage);
    },
    newIpp(newIpp){
      this.ipp=parseInt(newIpp);
      console.log(newIpp);
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
