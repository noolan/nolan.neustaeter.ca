<template>
  <section id="timeline">
    <div class="container">
      <div v-for="point in points">
        <aside v-if="point !== ''" v-html="point"></aside>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'timeline',
  props: {
    events: {
      type: Object,
      required: true
    }
  },
  computed: {
    points () {
      let lastEventKey = Object.keys(this.events).pop()
      let points = []
      for (let point = 0; point <= lastEventKey; point++) {
        points.push(this.events[point] || '')
      }
      return points
    }
  }
}
</script>

<style lang="scss">
@import '../styles/variables.scss';

#app {
  // general and mobile
  #timeline {
    padding-bottom: 2.5em;

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
