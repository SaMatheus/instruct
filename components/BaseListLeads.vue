<template>
  <div class="list">
    <ul class="list__ul" v-for="lead in leads" :key="lead.id">
      <li @click="itemToShow = lead.id; setVisibilityList();">
        <span>{{ lead.id }}</span>
        <p>{{ lead.name }}</p>
        <p>{{ lead.company.name }}</p>
      </li>
      <div v-if="itemToShow == lead.id && isVisible" class="list__insideList">

          <p>
            Phone: <strong>{{ lead.phone }}</strong>
          </p>
          <p>
            E-mail: <strong>{{ lead.email }}</strong>
          </p>
        </div>
    </ul>
  </div>
</template>

<script>
export default {
  components: true,
  props: {
    leads: { type: Array, required: true }
  },
  data () {
    return {
      show: false,
      isVisible: false,
      itemToShow: -1,
      isActive: false
    }
  },
  methods: {
    showList () {
      this.show = true
    },
    setVisibilityList () {
      this.isVisible = !this.isVisible
    }
  }
}
</script>

<style lang="scss" scoped>
.list {
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

      /* SPACING */
      margin-bottom: 1rem;

      /* POSITION */
      position: relative;

      /* EFFECT */
      transition: all 0.4s ease-out;
      cursor: pointer;

      &:hover {
        /* POSITION */
        padding-left: 2rem;
      }

      @media (max-width: 600px) {
        &:hover {
        /* POSITION */
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
        border-radius: 0.5rem 0 0 0.5rem;

        /* FONT */
        font: 1.5rem "trebuchet MS", "lucida sans";
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

        /* SPACING */
        margin-left: 0.2rem;
        padding-left: 2rem;

        &:nth-last-child(1) {
          /* BOX-MODEL */
          border-radius: 0 0.5rem 0.5rem 0;

          /* SPACING */
          margin-left: 0;
          padding-left: 0;
        }
      }
    }
  }
}
</style>
