<template>
    <div class="layout">
        <navigation :add-entry.sync="addEntry"></navigation>
        <entry-add :show.sync="addEntry"></entry-add>
        <router-view></router-view>
        <footer-view></footer-view>
    </div>
</template>

<style lang="sass">
    @import "settings";
    @import "~foundation-sites/scss/typography/base";
    @import "~font-awesome/scss/path";

    @include foundation-global-styles;
    @include foundation-typography-base;

    .layout {
        width: rem-calc(1200);
        margin: 0 auto;
    }
</style>

<script type="text/babel">
    import store            from 'vuex/store'
    import Mousetrap        from 'mousetrap'
    import Navigation       from 'components/navigation.vue'
    import EntryAdd         from 'components/entry-add.vue'
    import FooterView       from 'components/footer.vue'
    import {fetchEntries}   from 'vuex/actions'

    export default {
        store,

        vuex: {
            actions: {
                fetchEntries
            }
        },

        components: {
            Navigation,
            EntryAdd,
            FooterView
        },

        data() {
            return {
                addEntry: false
            }
        },

        created() {
            this.fetchEntries()

            Mousetrap.bind('a e', function () {
                this.addEntry = true
                return false
            }.bind(this))

            Mousetrap.bind('esc', function () {
                this.addEntry = false
                return false
            }.bind(this))
        }
    }
</script>