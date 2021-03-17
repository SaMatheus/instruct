<template>
  <div class="list">
    <header>
      <p>Name</p>
      <p>Company category</p>
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
        <p>{{ lead.company.bs }}</p>
      </li>
      <div
        v-if="itemToShow == lead.id && isVisible"
        class="
          list__insideList
        "
      >
        <div>
          <p>Company</p>
          <strong>{{ lead.company.name }}</strong>
        </div>
        <div>
          <p>Username</p>
          <strong>{{ lead.username }}</strong>
        </div>
        <div>
          <p>Phone</p>
          <strong>
            <a :href="`tel:+${lead.phone}`" target="_blank">
              {{ lead.phone }}
            </a>
          </strong>
          <p>open on your smartphone</p>
        </div>
        <div>
          <p>E-mail</p>
          <strong>
            <a :href="`mailto:${lead.email}`" target="_blank">
              {{ lead.email }}
            </a>
          </strong>
          <p>send an email now</p>
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
          <p>click to open in Google Maps</p>
        </div>
        <div>
          <p>Website</p>
          <strong>
            <a :href="`http://${lead.website}`" target="_blank">
              {{ lead.website }}
            </a>
          </strong>
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
  margin-top: 3rem;

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
      /* TEXT */
      font-size: 1.2rem;
      line-height: 2rem;
      &:nth-child(1) {
        padding-left: 8px;
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

      /* TEXT */
      text-transform: capitalize;

      &:hover {
        /* BOX-MODEL */
        padding-left: 2rem;
      }

      @media (max-width: 800px) {
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

        @media (max-width: 420px) {
          height: 5rem;
        }
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
        margin-left: 0.5rem;
        padding-left: 1rem;
        padding-right: 1.5rem;

        /* POSITION */
        position: relative;

        &:after {
          content: '';
          display: inline-block;
          height: 40%;
          width: 1px;
          background: $text;
          position: absolute;
          right: 1rem;
          opacity: 0.2;
        }

        &:nth-last-child(1) {
          /* BOX-MODEL */
          border-radius: 0 0.3rem 0.3rem 0;
          margin-left: 0;
          padding-left: 0;

          &:after {
            display: none;
          }
        }

        @media (max-width: 420px) {
          padding-left: 0.2rem;
          height: 5rem;
          &:nth-last-child(1) {
            padding: 0;
          }
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
    gap: 1rem 0.5rem;
    margin: -1.5rem 0 1rem 0;
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
      p:nth-last-child(1) {
        font-size: 0.5rem;
        opacity: 0.5;
      }

      a,
      strong {
        color: $dark-blue;
        text-decoration: none;
      }
    }

    @media (max-width: 420px) {
      grid-template-columns: 1fr;
    }
  }
}
</style>
