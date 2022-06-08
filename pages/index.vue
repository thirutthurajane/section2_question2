<template>
  <div>
  <input type="text"
         placeholder="Filter Categories"
         v-model="filter" />
    <table>
    <tbody v-if="filteredData !== null || filteredData.length > 0">
      <tr v-for="(row, index) in filteredData" :key="`${index}`">
        <span>{{ row }}</span>
      </tr>
    </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      categories: [],
      filter: ''
    }
  },
  computed: {
    filteredData() {
      if(this.filter !== '') {
        return  this.categories.filter((row) => {
          console.log(row)
          return row.toLowerCase().includes(this.filter.toLowerCase());
        });
      } else {
        return this.categories;
      }
    }
  },
  async fetch() {
    let res = await this.$axios.get('https://api.publicapis.org/categories');
    console.log(res.data)
    this.categories = res.data.categories;
  }
}
</script>
