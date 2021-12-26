<template>
  <div class="container my-5">
    <user-search-form></user-search-form>
    <b-table :data="userss" :columns="columns"></b-table>
    <b-pagination
      :total="total"
      v-model="current"
      :range-before="rangeBefore"
      :range-after="rangeAfter"
      :order="order"
      :size="size"
      :simple="isSimple"
      :rounded="isRounded"
      :per-page="perPage"
      :icon-prev="prevIcon"
      :icon-next="nextIcon"
      aria-next-label="Next page"
      aria-previous-label="Previous page"
      aria-page-label="Page"
      aria-current-label="Current page"
    >
    </b-pagination>
  </div>
</template>

<script lang="ts">
import Vue from "vue"
import titanic from "@/assets/titanic.json"
import UserSearchForm from "@/components/parts/UserSearchForm.vue"
import { bus } from "../main"

export default Vue.extend({
  components: { UserSearchForm },
  name: "Home",
  data() {
    return {
      users: titanic,
      columns: [
        {
          field: "name",
          label: "Name",
        },
        {
          field: "sex",
          label: "Sex",
        },
        {
          field: "age",
          label: "Age",
        },
      ],
      total: 200,
      current: 1,
      perPage: 10,
      rangeBefore: 3,
      rangeAfter: 1,
      order: "",
      size: "",
      isSimple: false,
      isRounded: false,
      prevIcon: "chevron-left",
      nextIcon: "chevron-right",
    }
  },
  computed: {
    userss(): Array {
      // const a
      return this.users.slice((this.current - 1) * this.perPage, this.current * this.perPage)
    },
  },
  mounted() {
    this.userData()
  },
  methods: {
    userData() {
      bus.$on("changedUserData", (data) => {
        console.log(data)
        this.users = data
        this.total = this.users.length
      })
    },
    // pagination() {

    // }
  },
})
</script>
