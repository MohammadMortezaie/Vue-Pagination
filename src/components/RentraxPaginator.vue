<template>
  <div class="row">
    <nav aria-label="Page navigation example">
      <ul class="pagination">
        <!-- pagination left -->
        <li class="page-item" v-if="page != 1">
          <a href="#" @click="prevPage" rel="prev" class="page-link">«</a>
        </li>
        <li class="page-item disabled" v-else>
          <span class="page-link">«</span>
        </li>
        <!-- End -->
        <!-- Show All  -->
        <template v-if="paginationCount <= numberShowAll">
          <RangeLoop :page="page" :start="1" :end="paginationCount" @change-page="(n) => newPage(n)" />
        </template>
        <!-- End Show All  -->

        <!-- Loop for First number -->
        <template v-else-if="page <= halfPaginationShowCount">
          <RangeLoop :page="page" :start="1" :end="number" @change-page="(n) => newPage(n)" />
          <li class="page-item disabled"><span class="page-link">...</span></li>
          <RangeLoop :page="page" :start="paginationCount - numberCountFirstAndEnd + 1" :end="paginationCount"
            @change-page="(n) => newPage(n)" />
        </template>
        <!-- End Loop for First number -->

        <!-- Loop for Middle number -->
        <template v-else-if="
          page > halfPaginationShowCount &&
          paginationCount - halfPaginationShowCount + 1 > page
        ">
          <RangeLoop :page="page" :start="1" :end="numberCountFirstAndEnd" @change-page="(n) => newPage(n)" />

          <li class="page-item disabled"><span class="page-link">...</span></li>

          <li class="page-item active">
            <a href="" rel="prev" class="page-link">{{ page }}</a>
          </li>

          <li class="page-item disabled"><span class="page-link">...</span></li>

          <RangeLoop :page="page" :start="paginationCount - numberCountFirstAndEnd + 1" :end="paginationCount"
            @change-page="(n) => newPage(n)" />
        </template>
        <!-- End Loop for Middle number -->

        <!-- Loop for End number -->
        <template v-else>
          <RangeLoop :page="page" :start="1" :end="numberCountFirstAndEnd" @change-page="(n) => newPage(n)" />
          <li class="page-item disabled"><span class="page-link">...</span></li>
          <RangeLoop :page="page" :start="paginationCount - number + 1" :end="paginationCount"
            @change-page="(n) => newPage(n)" />
        </template>
        <!-- End Loop for End number -->

        <!-- pagination right -->
        <li class="page-item" v-if="page < paginationCount">
          <a href="#" rel="prev" class="page-link" @click="nextPage">»</a>
        </li>
        <li class="page-item disabled" v-else>
          <span class="page-link">»</span>
        </li>
        <!-- End -->
      </ul>
    </nav>
  </div>
</template>

<script>
import RangeLoop from "./RangeLoop.vue";
export default {
  name: "RentraxPaginator",
  props: {
    productsCount: Number,
    numberCountFirstAndEnd: Number,
    paginationShowCount: Number,
    numberShowAll: Number,
    ipp: {
      type: Number,
      default: 5
    },
  },
  data() {
    return {
      page: 1,
      pageUrl: "http://localhost:8080/",
    };
  },
  components: {
    RangeLoop,
  },
  methods: {
    nextPage() {
      this.page += 1;
      this.$emit('changePage', this.page);
    },
    prevPage() {
      this.page -= 1;
      this.$emit('changePage', this.page);
    },
    newPage(pageNumber) {
      this.page = pageNumber;
      this.$emit('changePage', pageNumber);
    },
  },
  computed: {
    number: {
      get() {
        return this.numberShowAll + 1;
      },
    },
    paginationCount: {
      get() {
        return Math.round(this.productsCount / this.ipp);
      },
    },
    halfPaginationShowCount: {
      get() {
        return Math.round(this.paginationShowCount / 2);
      },
    },
    numberMiddlePagination: {
      get() {
        return Math.round(this.halfPaginationShowCount / 2);
      },
    },
  },
  watch: {
    ipp(val) {
      if (val) {
        this.page = 1
      }
    }
  },
};
</script>

