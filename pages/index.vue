<template>
  <div id="app" class="leads">
    <Logo />
    <!-- <Logo dark-background /> -->
    <h1 class="leads__title">Leads</h1>
    <div class="leads__filter">
      <label for="searchForName">
        <p>Name</p>
        <input
          id="searchForName"
          type="text"
          v-model.trim="search"
          placeholder="Search here"
        />
        <span>Search for name, phone or email</span>
      </label>
      <label for="searchForCompany">
        <p>Company</p>
        <input
          id="searchForCompany"
          type="text"
          v-model.trim="search"
          placeholder="Search here"
        />
        <span>Search for company name or category</span>
      </label>
    </div>
    <BaseListLeads :leads="searchLeadsResult" />
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'app',
  data() {
    return {
      search: null,
      leads: []
    }
  },
  mounted() {
    this.getData()
  },
  methods: {
    async getData() {
      await axios('https://jsonplaceholder.typicode.com/users').then(
        response => {
          this.leads = response.data
        }
      )
    }
  },
  computed: {
    searchLeadsResult() {
      if (this.search) {
        return this.leads.filter(lead => {
          const phone = this.search
            .toLowerCase()
            .split(' ')
            .every(valid => lead.phone.toLowerCase().includes(valid))
          const email = this.search
            .toLowerCase()
            .split(' ')
            .every(valid => lead.email.toLowerCase().includes(valid))
          const name = this.search
            .toLowerCase()
            .split(' ')
            .every(valid => lead.name.toLowerCase().includes(valid))
          const bs = this.search
            .toLowerCase()
            .split(' ')
            .every(valid => lead.company.bs.toLowerCase().includes(valid))
          if (phone) {
            return phone
          }
          if (email) {
            return email
          }
          if (name) {
            return name
          } else {
            return bs
          }
        })
      }
      return this.leads
    }
  }
}
</script>

<style lang="scss" scoped>
.leads {
  &__title {
    /* BOX MODEL */
    margin: 1.4rem 0;
    padding: 1.4rem 0;
    border-top: $border-color 1px solid;
  }
  &__filter {
    /* BOX MODEL */
    display: grid;
    grid-template-columns: 1fr 1fr;
    align-items: center;
    gap: 0 2rem;
    margin: 1rem 0;
    padding: 1rem;
    border-radius: 0.3rem;

    /* SIZE */
    max-width: 550px;
    min-width: 300px;

    /* COLOR */
    background-color: $light-blue;

    label {
      /* BOX MODEL */
      height: 100%;
      display: flex;
      flex-direction: column;
      p {
        /* COLOR */
        color: $grey;
        /* SIZE */
        margin-bottom: 4px;
      }
      input {
        /* SIZE */
        height: 40px;
        width: 100%;

        /* BOX MODEL */
        padding: 0 0.5rem;
        border: 0;
        border-radius: 0.3rem;

        /* TEXT */
        font-size: 1rem;

        /* COLRO */
        color: $text;
      }
      span {
        /* BOX MODEL */
        margin-top: 4px;

        /* COLOR */
        color: $grey;

        /* TEXT */
        font-size: 0.3rem;
      }
    }
  }
}
</style>
