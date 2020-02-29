<template>
    <div class="search">
        <div class="container">
            <div class="search__container">
                <div class="search__text">
                    Aranan kelime: {{searhPath}}
                </div>
                <form method="GET" action="ara" class="search__icontainer">
                    <input type="text" placeholder="Ne Arıyorsun?" name="q" class="search__input js-search-input" :value="searhPath" required/>
                    <button class="search__btn js-search-btn">Ara</button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Searchbar',
  props: ['searhPath']
}
</script>

<style lang="sass">
    .search
        margin-bottom: 10px
        padding: 30px 0
        background: #f1f1f1

        &__container
            padding: 0 15px

        &__icontainer
            position: relative

        &__input
            width: 100%
            padding: 10px 20px
            border: 1px solid #eee

        &__btn
            border: 0
            background: none
            position: absolute
            right: 0
            top: 0
            padding: 11px
            cursor: pointer

        &__text
            margin-bottom: 10px
            font-size: 14px
            color: #333

        &__detail
            padding: 0 15px

        &__warning
            background: #FEEFB3
            color: #9F6000
            border-radius: 3px
            padding: 10px
            margin: 10px 0

        &__ritem
            padding: 10px 0
            border-bottom: 1px solid #eee

            &:last-child
                border: 0

        &__cname
            margin-bottom: 5px
            color: #333
            font-size: 16px

        &__cadress
            margin-bottom: 5px
            color: #333
            font-size: 14px

        &__find
            padding: 15px 0
            font-size: 13px
            color: #333
            display: flex
            align-items: center
            justify-content: space-between
            margin: 0 -15px

        &__ftext
            padding: 0 15px
            display: flex
            align-items: center

        &__mark
            background: #007eff
            min-width: 1.6rem
            min-height: 1.2rem
            text-align: center
            font-size: .75rem
            font-weight: 500
            color: #FFF
            display: flex
            align-items: center
            justify-content: center
            padding: 0 6px
            border-radius: 4px
            margin-right: 5px

        &__more
            background: #007eff
            color: #FFF
            cursor: pointer
            padding: 15px 30px
            border: 0
            border-radius: 4px
            margin: 15px 0

</style>
