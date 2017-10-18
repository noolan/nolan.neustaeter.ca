<template>
  <section id="knowledge">
    <div>
      <h2 class="heading">Languages and Frameworks and Platforms.<br>Oh my!</h2>

      <div class="search">
        <input type="text" v-model="search" :placeholder="placeholder" />
      </div>

      <div v-for="area of filtered_expertise" class="area">
        <div class="container">
        <h3>{{ area.title }}</h3>

          <div class="columns columns-wrap">
            <div v-for="category of area.categories" class="category">
              <h4>{{ category.title }}</h4>
              <ul>
                <li v-for="item of category.items">
                  <span class="item">{{ item }}</span>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>

      <h3 v-if="filtered_expertise.length === 0" class="no-results">
        Sorry, there are no results for your search term{{ search_terms.length > 0 ? 's' : '' }}
      </h3>

    </div>
  </section>
</template>

<script>
export default {
  name: 'knowledge',
  props: {
    expertise: {
      type: Array,
      required: true
    },
    placeholder: {
      type: String,
      required: false,
      default: 'Search for specific skills...'
    }
  },
  data() {
    return {
      search: ''
    };
  },

  computed: {
    search_terms: function() {
      if (this.search === '') {
        return [];
      } else {
        return this.search.trim().toLowerCase().split(' ')
      }
    },
    filtered_expertise: function() {
      let expertise = [];

      if (this.search === '') {
        expertise = this.expertise;
      } else {

        for (let area of this.expertise) {
          let matching_categories = [];

          for (let category of area.categories) {

            let matching_items = category.items.filter((function(item) {
              let lower_case_item = item.toLowerCase();
              return this.search_terms.some(function(term) {
                return lower_case_item.includes(term);
              });
            }).bind(this));

            if (matching_items.length) {
              matching_categories.push({
                title: category.title,
                items: matching_items
              });
            }
          } // end categories loop

          if (matching_categories.length) {
            expertise.push({
              title: area.title,
              categories: matching_categories
            })
          }
        } // end areas loop
      }

      return expertise;
    }
  }
}
</script>

<style lang="scss">
@import '../styles/variables.scss';

#app {
  #knowledge {

    padding-bottom: 0;

    .search {
      padding-bottom: 2em;
    }

    .area {
      padding: 2.5em 0;

      h3 {
        color: $medium;
      }

      .category {
        padding: 1.5rem .5rem;
        max-width: 25rem;

        h4 {
          border-bottom: 1px solid $lighter;
          text-align: center;
          padding-bottom: .1em;
          margin-bottom: .3em;
        }


        ul {
          columns: 10rem auto;
          list-style-type: none;
          padding-left: 0;

          li {
            display: block;
            padding: .25em .25em;
            line-height: 1.15;
          }
        }
      }
    }

    .area:nth-child(odd) {
      background-color: $lighter;

      .category {
        h4 {
          border-bottom: 1px solid $light;
        }
      }
    }

    .no-results {
      text-align: center;
      margin-bottom: 2em;
      color: $medium;
    }
  }
}
</style>
