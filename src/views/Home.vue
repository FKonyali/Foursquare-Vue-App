<template>
  <div>
    <SearchBox/>
    <div class="container">
      <Categories :allCategories="categories"/>
    </div>
  </div>
</template>

<script>
import SearchBox from '@/components/SearchBox.vue'
import Categories from '@/components/Categories.vue'

export default {
  name: 'Home',
  components: {
    SearchBox,
    Categories
  },
  data() {
    return {
        categories: ''
    }
  },
  created() {
    fetch('https://api.foursquare.com/v2/venues/categories?v=20170211&oauth_token=QEJ4AQPTMMNB413HGNZ5YDMJSHTOHZHMLZCAQCCLXIX41OMP&includeSupportedCC=true', 
    {
      headers: {
        'Accept-Language': 'tr',
      }
    })
    .then(data => data.json())
    .then(json => {
        this.categories = json.response.categories;
    });
  }
}
</script>

<style lang="sass">
  .container
    width: 860px
    margin: 0 auto
    max-width: 100%
    padding: 0 30px
</style>