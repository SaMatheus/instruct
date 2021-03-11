<template>
  <div id="app" class="leads">
    <Logo />
    <!-- <Logo dark-background /> -->
    <h1 class="leads__title">Leads</h1>
    <div class="leads__filter">
      <input name="search" type="text" v-model.trim="search" placeholder="Procure aqui">
    </div>
    <table v-if="leads.length" class="leads__table">
      <thead>
        <tr>
          <td></td>
          <td><h1>Cliente</h1></td>
          <td><h1>Contato</h1></td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="lead in searchResult" :key="lead.id">
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
    searchResult () {
      if (this.search) {
        return this.leads.filter((lead) => {
          return this.search.toLowerCase().split(' ').every(valid => lead.name.toLowerCase().includes(valid))
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
