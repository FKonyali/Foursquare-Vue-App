<template>
    <div>
        <div class="categories" v-if="allCategories">
            <div class="categories__box" v-for="item in allCategories" :key="item.id" :data-search="item.name" v-on:click="dataSearch">
                <h5 class="categories__title">{{item.name}}</h5>
                <img :src="item.icon.mapPrefix + item.icon.suffix" :alt="item.name">
            </div>
        </div>
        <div class="loading" v-if="!allCategories"> {{loading}} </div>
    </div>
</template>

<script>
export default {
  name: 'Categories',
  props: ['allCategories'],
  methods: {
      dataSearch: function(e) {
        let attr = e.currentTarget.getAttribute('data-search');
        document.querySelector('.js-search-input').value = attr;
        document.querySelector('.js-search-btn').click();
      }
  },
  data() {
      return {
          loading: 'Yükleniyor...'
      }
  }
}
</script>

<style lang="sass">
    h1
        font-size: 34px

    h2
        font-size: 30px

    h3
        font-size: 26px

    h4
        font-size: 22px

    h5
        font-size: 18px
    
    h6
        font-size: 14px

    h1, h2, h3, h4, h5, h6
        font-weight: 700
        margin-bottom: 15px

    img
        max-width: 100%
        
    .categories
        display: flex
        flex-wrap: wrap
        margin: 0 -15px

        &__box
            display: flex
            align-items: center
            flex-direction: column
            width: 33.333%
            margin-bottom: 30px
            padding: 0 15px

        &__title
            text-align: center
            height: 100%

    [data-search]
        cursor: pointer

    .loading
        margin: 30px 0
        text-align: center
        
</style>
