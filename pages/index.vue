<template>
  <div id="app" class="leads">
    <Logo />
    <!-- <Logo dark-background /> -->
    <h1 class="leads__title">Leads</h1>
    <div class="leads__filter">
      <input name="search" type="text" v-model.trim="search" placeholder="Procure aqui">
    </div>
      <BaseListLeads :leads="searchLeadsResult" />
  </div>
</template>

<script>
import axios from 'axios'
// import BaseList from '~/components/BaseList.vue'
export default {
  name: 'app',
  data () {
    return {
      search: null,
      leads: []
    }
  },
  mounted () {
    this.getData()
  },
  methods: {
    async getData () {
      await axios.get('https://jsonplaceholder.typicode.com/users').then((response) => {
        this.leads = response.data
      })
    }
  },
  computed: {
    searchLeadsResult () {
      if (this.search) {
        return this.leads.filter((lead) => {
          const phone = this.search.toLowerCase().split(' ').every(valid => lead.phone.toLowerCase().includes(valid))
          const email = this.search.toLowerCase().split(' ').every(valid => lead.email.toLowerCase().includes(valid))
          const name = this.search.toLowerCase().split(' ').every(valid => lead.name.toLowerCase().includes(valid))
          const bs = this.search.toLowerCase().split(' ').every(valid => lead.company.bs.toLowerCase().includes(valid))
          if (phone) {
            return phone
          } if (email) {
            return email
          } if (name) {
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
    margin: 1.4rem 0;
    padding: 1.4rem 0;
    border-top: $border-color 1px solid;
  }
  &__filter {
    margin: 1.4rem 0;
  }
}
</style>
