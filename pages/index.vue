<template>
  <div class="leads">
    <Logo />
    <!-- <Logo dark-background /> -->
    <h1 class="leads__title">Leads</h1>
    <div class="leads__filter">
      <input name="search" type="text" v-model.trim="search">
      <button type="submit">Procurar</button>
    </div>
    {{search}}
    <table class="leads__table">
      <thead>
        <tr>
          <td></td>
          <td><h1>Cliente</h1></td>
          <td><h1>Contato</h1></td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="lead of searchResult" :key="lead.id">
          <td>{{ lead.id }}</td>
          <td>
            <p>Nome: {{ lead.name }}</p>
            <p>Empresa: {{ lead.company.name }}</p></td>
          <td>
            <p>Telefone: {{ lead.phone }}</p>
            <p>E-mail: {{ lead.email }}</p>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      leads: [],
      search: ''
    }
  },
  mounted () {
    this.getData()
  },
  methods: {
    filterLeadsData () {
      this.leads.map((lead) => { return console.log(lead.company.bs) })
    },
    async getData () {
      await axios.get('https://jsonplaceholder.typicode.com/users').then((response) => {
        this.leads = response.data
        this.filteredLeads = response.data
        console.log(response)
      })
    }
  },
  computed: {
    searchResult () {
      if (this.search) {
        return this.leads.filter((lead) => {
          return this.search.toLowerCase().split(' ').every(v => lead.title.toLowerCase().includes(v))
        })
      } else {
        return this.leads
      }
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
  &__table {
    border: 1px solid black;
    width: 100%;
    td {
      border: 1px solid black;
    }
  }
}
</style>
