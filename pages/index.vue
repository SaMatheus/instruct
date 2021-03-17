<template>
  <div id="app" class="leads">
    <Logo />
    <h1 class="leads__title">Leads</h1>
    <div class="leads__filter">
      <h3>Filters</h3>
      <div>
        <label for="searchForName">
          <p>Contact name</p>
          <input
            id="searchForName"
            type="text"
            v-model.trim="searchName"
            placeholder="Search"
          />
          <span>Search for lead name</span>
        </label>
        <label for="searchForCompany">
          <p>Company category</p>
          <input
            id="searchForCompany"
            type="text"
            v-model.trim="searchCompany"
            placeholder="Search"
          />
          <span>Search for company category</span>
        </label>
      </div>
    </div>
    <BaseListLeads :leads="searchResults" />
  </div>
</template>

<script>
import api from '../services/api'
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
      await api('users').then(response => {
        this.leads = response.data
      })
    }
  },
  computed: {
    searchNameResult() {
      if (this.searchName) {
        return this.leads.filter(lead => {
          const name = this.searchName
            .toLowerCase()
            .split(' ')
            .every(curr => lead.name.toLowerCase().includes(curr))
          return name
        })
      }
      return this.leads
    },
    searchCompanyResult() {
      if (this.searchCompany) {
        return this.leads.filter(lead => {
          const companyBs = this.searchCompany
            .toLowerCase()
            .split(' ')
            .every(valid => lead.company.bs.toLowerCase().includes(valid))
          return companyBs
        })
      }
      return this.leads
    },
    searchResults() {
      return this.searchName ? this.searchNameResult : this.searchCompanyResult
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
    background: $light-blue;

    h3 {
      /* COLOR */
      color: $green;

      /* TEXT */
      font-size: 2rem;

      /* BOX MODEL */
      margin-bottom: 8px;
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

        /* TEXT */
        font-size: 1.2rem;

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
