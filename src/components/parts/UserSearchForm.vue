<template>
  <div class="user-search-form">
    <div class="columns">
      <div class="column is-one-third"></div>
      <div class="column">
        <b-field label="Name">
          <b-input v-model="name"></b-input>
        </b-field>
      </div>
      <div class="column"></div>
    </div>
    <div class="columns">
      <div class="column is-one-third"></div>
      <div class="column">
        <b-field label="Age">
          <b-input v-model="age"></b-input>
        </b-field>
      </div>
      <div class="column"></div>
    </div>
    <div class="columns mb-3">
      <div class="column is-one-third"></div>
      <div class="column">
        <b-field label="Sex">
          <b-input v-model="sex"></b-input>
        </b-field>

        <b-button type="is-primary" @click="search()">Search</b-button>
      </div>
      <div class="column"></div>
    </div>
  </div>
</template>

<script>
import Vue from "vue"
import titanic from "@/assets/titanic.json"
import { bus } from "../../main.ts"

export default Vue.extend({
  name: "UserSearchForm",
  data() {
    return {
      users: titanic,
      sex: "",
      name: "",
      age: "",
    }
  },
  mounted() {
    // this.$root.$on("search", () => {
    //   return this.search()
    // })
  },
  methods: {
    search() {
      let nameFound = []
      if (this.name && this.sex && this.age) {
        console.log(this.name, this.sex, this.age)
        nameFound = this.users.filter((m) => m.name.includes(this.name) && m.sex === this.sex && m.age === Number(this.age))
      } else if (this.name && this.sex) {
        console.log(this.name, this.sex)
        nameFound = this.users.filter((m) => m.name.includes(this.name) && m.sex === this.sex)
      } else if (this.age && this.sex) {
        console.log(this.age, this.sex)
        nameFound = this.users.filter((m) => m.age === Number(this.age) && m.sex === this.sex)
      } else if (this.name && this.age) {
        console.log(this.name, this.age)
        nameFound = this.users.filter((m) => m.age === Number(this.age) && m.name.includes(this.name))
      } else {
        nameFound = this.users.filter((m) => m.name.includes(this.name) || m.sex === this.sex || m.age === Number(this.age))
      }

      bus.$emit("changedUserData", nameFound)
      // console.log(nameFound)
    },
  },
})
</script>

<style scoped>
.user-search-form {
  height: auto;
  background-color: yellow;
}
</style>
