<template>
  <div class="col-md-12">
    <div class="form-group">
      <input type="text" class="form-control" v-model="search" placeholder="Search">
    </div>
    <div class="table-responsive">
      <table class="table table-striped table-bordered" style="width:100%">
          <thead width="400px">
              <tr>
                  <th v-for="(header, col) in fileHeaders" :key="col" scope="col" @click="sort(header)">{{ header }}</th>
              </tr>
          </thead>
          <tbody>
              <tr v-for="(row, index) in fileData" :key="index">
                <td v-for="(colData, colIndex) in row" :key="colIndex">{{ colData }}</td>
              </tr>
          </tbody>
      </table>
    </div>
 <button @click="prevPage" class="float-left btn btn-outline-info btn-sm"><i class="fas fa-arrow-left"></i> Previous</button> 
 <button @click="nextPage" class="float-right btn btn-outline-info btn-sm">Next <i class="fas fa-arrow-right"></i></button>
  </div>
</template>

<script>
export default {
  data: () => ({
    users: [],
    currentSort: "name",
    currentSortDir: "asc",
    search: "",
    searchSelection: "",
    pageSize: 5,
    currentPage: 1
  }),

  props: {
    fileHeaders: {
      type: Array
    },
    fileData: {
      type: Array,
      required: false
    }
  },

  methods: {
    sort: function(s) {
      if (s === this.currentSort) {
        this.currentSortDir = this.currentSortDir === "asc" ? "desc" : "asc";
      }
      this.currentSort = s;
    },
    nextPage: function() {
      if (this.currentPage * this.pageSize < this.users.length)
        this.currentPage++;
    },
    prevPage: function() {
      if (this.currentPage > 1) this.currentPage--;
    }
  },

  // computed: {
  //   sortedActivity: function() {
  //     return this.users
  //       .sort((a, b) => {
  //         let modifier = 1;
  //         if (this.currentSortDir === "desc") modifier = -1;
  //         if (a[this.currentSort] < b[this.currentSort]) return -1 * modifier;
  //         if (a[this.currentSort] > b[this.currentSort]) return 1 * modifier;
  //         return 0;
  //       })
  //       .filter((row, index) => {
  //         let start = (this.currentPage - 1) * this.pageSize;
  //         let end = this.currentPage * this.pageSize;
  //         if (index >= start && index < end) return true;
  //       });
  //   },

  //   filteredList() {
  //     return this.users
  //       .filter(data => {
  //         let email = data.email.toLowerCase().match(this.search.toLowerCase());
  //         let name = data.name.toLowerCase().match(this.search.toLowerCase());
  //         let city = data.address.city
  //           .toLowerCase()
  //           .match(this.search.toLowerCase());
  //         let phone = data.phone.toLowerCase().match(this.search.toLowerCase());
  //         return email || name || city || phone;
  //       })
  //       .filter((row, index) => {
  //         let start = (this.currentPage - 1) * this.pageSize;
  //         let end = this.currentPage * this.pageSize;
  //         if (index >= start && index < end) return true;
  //       });
  //   }
  // }
};
</script>

<style>
th {
  cursor: pointer;
  /* width: 500px !important; */
  white-space: nowrap;
}

tr {
  white-space: nowrap;
}

textarea {
  width: 100%;
  overflow: scroll;
  overflow-x: scroll;
}
</style>
