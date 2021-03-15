<template>
  <div id="app" class="leads">
    <Logo />
    <!-- <Logo dark-background /> -->
    <h1 class="leads__title">Leads</h1>
    <div class="leads__filter">
      <h3>Filters</h3>
      <div>
        <label for="searchForName">
          <p>Name</p>
          <input
            id="searchForName"
            type="text"
            v-model.trim="searchName"
            placeholder="Search"
          />
          <span>Search for name, phone or email</span>
        </label>
        <label for="searchForCompany">
          <p>Company</p>
          <input
            id="searchForCompany"
            type="text"
            v-model.trim="searchCompany"
            placeholder="Search"
          />
          <span>Search for company name or category</span>
        </label>
      </div>
    </div>
    <BaseListLeads
      :leads="searchName ? searchNameResult : searchCompanyResult"
    />
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'app',
  data() {
    return {
      searchName: null,
      searchCompany: null,
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
    searchNameResult() {
      if (this.searchName) {
        return this.leads.filter(lead => {
          const name = this.searchName
            .toLowerCase()
            .split(' ')
            .every(valid => lead.name.toLowerCase().includes(valid))
          const phone = this.searchName
            .toLowerCase()
            .split(' ')
            .every(valid => lead.phone.toLowerCase().includes(valid))
          const email = this.searchName
            .toLowerCase()
            .split(' ')
            .every(valid => lead.email.toLowerCase().includes(valid))
          if (name) {
            return name
          }
          if (phone) {
            return phone
          } else {
            return email
          }
        })
      }
      return this.leads
    },
    searchCompanyResult() {
      if (this.searchCompany) {
        return this.leads.filter(lead => {
          const companyName = this.searchCompany
            .toLowerCase()
            .split(' ')
            .every(valid => lead.company.name.toLowerCase().includes(valid))
          const bs = this.searchCompany
            .toLowerCase()
            .split(' ')
            .every(valid => lead.company.bs.toLowerCase().includes(valid))
          if (companyName) {
            return companyName
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
    display: flex;
    flex-direction: column;
    gap: 0 2rem;
    margin: 1rem 0;
    padding: 1rem;
    border-radius: 0.3rem;

    /* SIZE */
    max-width: 550px;
    min-width: 200px;

    /* COLOR */
    background-color: $light-blue;

    h3 {
      /* COLOR */
      color: $green;

      /* TEXT */
      font-size: 2rem;

      /* BOX MODEL */
      margin-bottom: 16px;
    }

    div {
      /* BOX MODEL */
      display: grid;
      grid-template-columns: 1fr 1fr;
      align-items: center;
      gap: 0 2rem;
    }

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
        font-size: 14px;
      }
    }

    @media (max-width: 420px) {
      div {
        grid-template-columns: 1fr;
        gap: 1rem 0;
      }
    }
  }
}
</style>
