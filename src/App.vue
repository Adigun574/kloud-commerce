<template>
  <!-- <h1 class="text-3xl font-bold underline">
    Hello world!
  </h1> -->
  <div class="py-8 px-6 app-body">
    <Header />

    <TablePage />

    <!-- <Loader /> -->


    <!-- <pagination v-model="page" :records="500" @paginate="myCallback"/> -->






    <!-- <div class="mt-3">
      <b-table
        id="my-table"
        :items="items"
        :per-page="perPage"
        :current-page="currentPage"
        small
      ></b-table>
      <h6>Goto first and last button number</h6>
      <b-pagination
        v-model="currentPage"
        :total-rows="rows"
        :per-page="perPage"
        first-number
        last-number
      ></b-pagination>
    </div> -->

   

  </div>
</template>

<script>
// import Pagination from 'vue-pagination-2';
import Header from './components/Header.vue';
import TablePage from './components/TablePage.vue';
import Loader from './components/Loader.vue';


export default {

  data() {
    return {
      }
  },
  computed: {
  },
  created() {
  },
  mounted(){
  },
  methods: {
  },
  components: {
    // Pagination
    Header,
    TablePage,
    Loader
  }
}
</script>


<style scoped>
  /* *{
    color:#616469
  } */
  .app-body{
    background-color: #f4f5fa;
  }
  /* .kloud-div{
    background-color: #2a2a8f;
    color:white;
  } */
  th, td {
    padding: 15px;
  }

  /* PAGINATION */

</style>