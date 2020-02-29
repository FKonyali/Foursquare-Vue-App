<template>
    <div>
        <div class="search__ritem" v-for="(item, index) in newItem" :key="index">
            <div class="search__cname">
                {{index + (newsCount * 1) + 1}}) {{item.venue.name}}
            </div>
            <div class="search__cadress">
                {{item.venue.location.address}}
                {{item.venue.location.crossStreet}}
                {{item.venue.location.city}}
                {{item.venue.location.country}}
            </div>
            <div class="search__cmap">
                <iframe 
                    width="100%" 
                    height="170" 
                    frameborder="0" 
                    scrolling="no" 
                    marginheight="0" 
                    marginwidth="0" 
                    :src="'https://maps.google.com/maps?q=' + item.venue.location.lat + ',' + item.venue.location.lng + '&hl=es&z=14&amp;output=embed'"
                    >
                </iframe>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'SearchItem',
    props: ['newItem', 'newsCount']
}
</script>

<style>

</style>