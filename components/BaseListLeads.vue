<template>
  <div class="list">
    <header>
      <p>Name</p>
      <p>Company</p>
    </header>
    <ul class="list__ul" v-for="lead in leads" :key="lead.id">
      <li
        @click="
          itemToShow = lead.id
          setVisibilityList()
        "
      >
        <span>{{ lead.id }}</span>
        <p>{{ lead.name }}</p>
        <p>{{ lead.company.name }}</p>
      </li>
      <div
        v-if="itemToShow == lead.id && isVisible"
        class="
          list__insideList
        "
      >
        <div>
          <p>Username</p>
          <strong>{{ lead.username }}</strong>
        </div>
        <div>
          <p>Phone</p>
          <strong>{{ lead.phone }}</strong>
        </div>
        <div>
          <p>E-mail</p>
          <strong>{{ lead.email }}</strong>
        </div>
        <div>
          <p>Address</p>
          <a
            :href="
              `https://maps.google.com/?q=${lead.address.geo.lat},${lead.address.geo.lng}`
            "
            target="_blank"
          >
            <strong>
              {{ lead.address.suite }}
              {{ lead.address.street }},
              {{ lead.address.city }}
            </strong>
          </a>
          click to open in Google Maps
        </div>
        <div>
          <p>Website</p>
          <strong>{{ lead.website }}</strong>
        </div>
        <div>
          <p>Company category</p>
          <strong>{{ lead.company.bs }}</strong>
        </div>
      </div>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    leads: { type: Array, required: true }
  },
  data() {
    return {
      show: false,
      isVisible: false,
      itemToShow: -1,
      isActive: false
    }
  },
  methods: {
    showList() {
      this.show = true
    },
    setVisibilityList() {
      this.isVisible = !this.isVisible
    }
  }
}
</script>

<style lang="scss" scoped>
.list {
  header {
    /* BOX-MODEL */
    display: grid;
    grid-template-columns: 1fr 1fr;
    justify-content: space-evenly;

    /* SPACING */
    padding-left: 4rem;
    margin-bottom: 1rem;

    /* POSITION */
    position: relative;

    p {
      font-size: 1.5rem;
      line-height: 3rem;
      &:nth-child(1) {
        padding-left: 2.2rem;
      }
    }

    &:after {
      content: '';
      height: 1px;
      width: 100%;
      background: $border-color;
      position: absolute;
      bottom: 0;
      left: 0;
    }
  }

  &__ul {
    /* BOX-MODEL */
    display: flex;
    flex-direction: column;

    /* SPACING */
    gap: 1rem 0;

    li {
      /* COLORS */
      color: $text;

      /* BOX-MODEL */
      display: flex;
      margin-bottom: 1rem;

      /* POSITION */
      position: relative;

      /* EFFECT */
      transition: all 0.2s ease;
      cursor: pointer;

      &:hover {
        /* BOX-MODEL */
        padding-left: 2rem;
      }

      @media (max-width: 600px) {
        &:hover {
          /* BOX-MODEL */
          padding-left: 0;
        }
      }

      span {
        /* COLORS */
        background: $green;

        /* SIZE */
        height: 4rem;
        width: 100%;
        max-width: 4rem;
        min-width: 4rem;

        /* BOX-MODEL */
        display: flex;
        justify-content: center;
        align-items: center;
        border-radius: 0.3rem 0 0 0.3rem;

        /* FONT */
        font: 1.5rem 'trebuchet MS', 'lucida sans';
      }

      p {
        /* SIZE */
        height: 4rem;
        width: 100%;

        /* COLORS */
        background: $grey;

        /* BOX-MODEL */
        display: flex;
        justify-content: flex-start;
        align-items: center;
        border-radius: none;
        margin-left: 1.5rem;
        padding-left: 1rem;

        &:nth-last-child(1) {
          /* BOX-MODEL */
          border-radius: 0 0.3rem 0.3rem 0;
          margin-left: 0;
          padding-left: 0;
        }
      }

      a {
        color: $text;
        text-decoration: none;
      }
    }
  }

  &__insideList {
    /* COLOR */
    background: $grey;

    /* BOX-MODEL */
    display: grid;
    grid-template-columns: 1fr 1fr;
    align-items: center;
    gap: 0.5rem;
    margin: -1.8rem 0 1rem 0;
    padding: 1.5rem;
    border-radius: 0.5rem;

    /* EFFECT */
    transition: all 0.4s ease-out;

    div {
      h4 {
        color: $grey;
      }

      p {
        color: $text;
      }
      a,
      strong {
        color: $dark-blue;
        text-decoration: none;
      }
    }
  }
}
</style>
