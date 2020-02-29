<template>
    <div class="search-area">
        <SearchBox :searhPath="query"/>
        <div class="container">
            <div class="search__detail">
                <div class="loading" v-if="!newItem"> {{loading}} </div>
                <div class="search__warning" v-if="warning">
                    {{warning}}
                </div>
                <div class="search__find" v-if="totalResults">
                    <router-link to="/" title="Ana Sayfa" class="box__inner"> 
                        <span class="article__back">{{homeBackText}}</span> 
                    </router-link>
                    <div class="search__ftext">
                        <span class="search__mark">{{totalResults}}</span> sonuç bulundu
                    </div>
                </div>
                <SearchItem :newItem="newItem" :newsCount="0"/>
                <SearchItem :newItem="moreNewsItem" :newsCount="5"/>
                <div class="loading" v-if="moreBtnClicked">
                    {{moreNewsLoading}}
                </div>
                <div class="text-center" v-if="(pagination + 5) < totalResults && moreBtnClicked == false">
                    <button class="search__more" v-on:click="dataMore">
                        Daha fazla görüntüle (+5)
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import SearchBox from '@/components/SearchBox.vue'
import SearchItem from '@/components/SearchItem.vue'

export default {
  name: 'ContentDetail',
  props: ['newItem', 'warning', 'totalResults', 'loading', 'locationContent'],
  components: {
    SearchBox,
    SearchItem
  },
  data() {
    return {
        homeBackText: '< Ana Sayfaya Dön',
        query: decodeURIComponent(this.$route.fullPath.split('=')[1]),
        pagination: 0,
        moreNewsItem: [],
        moreNewsLoading: 'Yükleniyor...',
        moreBtnClicked: false
    }
  },
  methods: {
        dataMore: function() {
            this.moreBtnClicked = true;
            if(this.pagination < this.totalResults) {
                this.pagination += 5;
                this.moreDataCount++;
            }
            const query = this.$route.fullPath.split('=')[1];
            fetch('https://api.foursquare.com/v2/venues/explore?client_id=E2OGWGNVMZYOTYE1MDB54W2VLJQF3DRWETVD3N5AGMU5U4I1&client_secret=VPPSLFKCHEDYGKA0T45V4ZLOXGDOE230NTG1WWZK3R2T24JK&v=20180323&limit=5&ll='+ this.locationContent +'&query='+query + '&offset=' + this.pagination, 
            {
            headers: {
                'Accept-Language': 'tr',
            }
            })
            .then(data => data.json())
            .then(json => {
                this.moreNewsItem = [...this.moreNewsItem, ...json.response.groups[0].items]
                this.moreBtnClicked = false;
            });
        }
  }
}
</script>

<style lang="sass">
    .article
        &__img
            margin-bottom: 15px

            img
                width: 100%

        &__content
            p
                margin-bottom: 15px

        &__back
            color: #333
            text-decoration: underline
            padding: 0 15px
            font-size: 13px
            display: inline-block 

    .text-center
        text-align: center
</style>
