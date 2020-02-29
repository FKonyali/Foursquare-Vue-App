<template>
  <div>
    <ContentDetail :newItem="newsItem" :warning="warning" :totalResults="totalResults" :loading="loading" :locationContent="locationContent"/>
  </div>
</template>

<script>
import ContentDetail from '@/components/ContentDetail.vue'

export default {
  name: 'Detail',
  components: {
    ContentDetail
  },
  data() {
    return {
        newsItem: '',
        warning: '',
        totalResults : '',
        locationStatus: '',
        locationContent: '41.0054958,28.8720984',
        loading: 'Yükleniyor...'
    }
  },
  created() {
    this.getLocation();
  },
  methods: {
    getLocation: function() {
      let _this = this;
      function success(position) {
        const latitude  = position.coords.latitude;
        const longitude = position.coords.longitude;

        _this.locationContent = (latitude + ',' + longitude);
        _this.fetchData();
      }

      function error(error) {
        switch(error.code) {
          case error.PERMISSION_DENIED:
            _this.locationStatus = "Konum bilgisini tarayıcınız reddediyor."
            break;
          case error.POSITION_UNAVAILABLE:
            _this.locationStatus = "Konum bilgisi mevcut değil."
            break;
          case error.TIMEOUT:
            _this.locationStatus = "Kullanıcı konum bilgisi zaman aşımına uğradı."
            break;
          case error.UNKNOWN_ERROR:
            _this.locationStatus = "Bilinmeyen bir hata oluştu."
            break;
        }

        setTimeout(() => {
          _this.fetchData();
        }, 1000);

        _this.loading = _this.locationStatus
      }

      if (!navigator.geolocation) {
        _this.locationStatus = 'Konum çekme özelliği tarayıcınız tarafından desteklenmiyor';
      } else {
        _this.locationStatus = 'Konuma erişiliyor…';
        navigator.geolocation.getCurrentPosition(success, error);
      }
    },
    fetchData: async function() {
      const query = this.$route.fullPath.split('=')[1];

      await fetch('https://api.foursquare.com/v2/venues/explore?client_id=E2OGWGNVMZYOTYE1MDB54W2VLJQF3DRWETVD3N5AGMU5U4I1&client_secret=VPPSLFKCHEDYGKA0T45V4ZLOXGDOE230NTG1WWZK3R2T24JK&v=20180323&limit=5&ll='+ this.locationContent +'&query='+query, 
      {
        headers: {
          'Accept-Language': 'tr-TR',
        }
      })
      .then(data => data.json())
      .then(json => {
          this.newsItem = json.response.groups[0].items;
          this.warning = json.response.warning ? json.response.warning.text : '';
          this.totalResults = json.response.totalResults;
      })
    }
  }
}
</script>