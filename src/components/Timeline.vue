<template>
  <section id="timeline">
    <div class="container">
      <div v-for="year in all_years">
        <aside v-if="year !== ''" v-html="year"></aside>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'timeline',
  props: {
    years: {
      type: Number,
      required: true
    },
    events: {
      type: Object,
      required: true
    }
  },
  computed: {
    all_years: function() {
      let all_years = [];
      for (let year = this.years; year >= 0; year--) {
        all_years.push(this.events[year] || '');
      }

      return all_years;
    }
  }
}
</script>

<style lang="scss">
@import '../styles/variables.scss';

#app {
  // general and mobile
  #timeline {


    > .container {
      border-bottom: 2px solid $dark;
      margin: 80px auto;
      width: calc(100% - 80px);

      display: none;
      justify-content: space-around;
      flex-direction: column;

      > div {
        position: relative;
        display: inline-block;
      }

      > div::before {
        content: "";
        position: absolute;
        height: 15px;
        border-right: 2px solid $dark;
        display: inline-block;
      }

      > div:nth-child(odd)::before {
        bottom: 0;
      }
      > div:nth-child(even)::before {
        bottom: -16px;
      }

      > div > aside {
        position: absolute;
        font-size: 10px;
        text-align: center;
        left: 0;
        transform: translateX(-50%);
        line-height: 1.1;
      }

      > div:nth-child(odd) > aside {
        bottom: 22px;
      }
      > div:nth-child(even) > aside {
        top: 20px;
      }
    }
  }


  // desktop only
  @media (min-width: $desktop-width) {
    #timeline {

      > .container {
        display: flex;
        border-bottom: 2px solid $dark;
        margin: 80px auto;
        width: calc(100% - 80px);

        flex-direction: row;

        > div {
          position: relative;
          display: inline-block;
        }

        > div::before {
          content: "";
          position: absolute;
          height: 15px;
          border-right: 2px solid $dark;
          display: inline-block;
        }

        > div:nth-child(odd)::before {
          bottom: 0;
        }
        > div:nth-child(even)::before {
          bottom: -16px;
        }

        > div > aside {
          position: absolute;
          font-size: 10px;
          text-align: center;
          left: 0;
          transform: translateX(-50%);
          line-height: 1.1;
        }

        > div:nth-child(odd) > aside {
          bottom: 22px;
        }
        > div:nth-child(even) > aside {
          top: 20px;
        }
      }
    }
  }
}
</style>
