<template>
  <div class="search__box">
    <input type="text" placeholder="kogo szukasz?" v-model="searchQuery" />
    <div
      class="search__box__items"
      v-for="(item, index) in searchByLastName"
      :key="index"
    >
      <p>{{ item.last_name }}</p>
      <img :src="item.avatar" />
    </div>
  </div>
</template>
<script>
export default {
  name: "SearchPhoto",
  data() {
    return {
      qwe: [],
      searchQuery: ""
    };
  },

  methods: {
    fetchUsers() {
      //   this.$http.get("https://reqres.in/api/users?page=2").then(response => {
      //     this.responseData = response.data.data;
      //     console.og(response.data.data);
      //   });
      let cmp = this;
      this.axios.get("https://reqres.in/api/users?page=2").then(response => {
        console.log(response.data.data);
        cmp.qwe = response.data.data;
      });
    }
  },
  created() {
    this.fetchUsers();
  },
  computed: {
    searchByLastName() {
      if (this.searchQuery.length !== 0) {
        return this.qwe.filter(item => {
          return (
            item.last_name
              .toLowerCase()
              .indexOf(this.searchQuery.toLowerCase()) > -1
          );
        });
      }
      return [];
    }
  }
};
</script>
<style lang="scss">
.search__box__items {
  width: 10rem;
  height: auto;
}
</style>
