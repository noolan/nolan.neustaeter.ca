<template>
  <section id="knowledge">
    <div>
      <h2 class="heading">Languages and Frameworks and Platforms.<br><em>Oh my!</em></h2>

      <div class="search">
        <label for="knowledge_search">Search</label><input id="knowledge_search" aria-label="Search" type="text" v-model="search" :placeholder="placeholder" />
      </div>

      <div v-for="(area, areaIndex) of filteredExpertise" :key="areaIndex" class="area">
        <div class="container">
        <h3>{{ area.title }}</h3>

          <div class="columns columns-wrap">
            <div v-for="(category, categoryIndex) of area.categories" :key="categoryIndex" class="category">
              <h4>{{ category.title }}</h4>
              <ul>
                <li v-for="(item, itemIndex) of category.items" :key="itemIndex">
                  <span class="item">{{ item }}</span>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>

      <h3 v-if="filteredExpertise.length === 0" class="no-results">
        Sorry, there are no results for your search term{{ searchTerms.length > 0 ? 's' : '' }}
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
  data () {
    return {
      search: ''
    }
  },

  computed: {
    searchTerms () {
      if (this.search === '') {
        return []
      } else {
        return this.search.trim().toLowerCase().split(' ')
      }
    },
    filteredExpertise () {
      let expertise = []

      if (this.search === '') {
        expertise = this.expertise
      } else {
        for (let area of this.expertise) {
          let matchingCategories = []

          for (let category of area.categories) {
            let matchingItems = category.items.filter(function (item) {
              let lowerCaseItem = item.toLowerCase()
              return this.searchTerms.some(function (term) {
                return lowerCaseItem.includes(term)
              })
            }.bind(this))

            if (matchingItems.length) {
              matchingCategories.push({
                title: category.title,
                items: matchingItems
              })
            }
          } // end categories loop

          if (matchingCategories.length) {
            expertise.push({
              title: area.title,
              categories: matchingCategories
            })
          }
        } // end areas loop
      }

      return expertise
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
      label {
        display: none;
      }
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

@media print {
  #knowledge {
    .heading {
      em {
        display: none;
      }
    }
  }
}

</style>
