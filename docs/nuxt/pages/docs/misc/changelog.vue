<template>
    <div class="container bd-content" v-html="readme"></div>
</template>

<script>
    import layout from '../../../layouts/docs.vue';
    import readme from '../../../../../CHANGELOG.md';

    export default {
        components: {layout},
        layout: 'docs',
        computed: {
            readme() {
                return readme;
            }
        },
        created() {
            // We remove the h3 tags because the all have the same generated ID
            this.$root.$emit('bv-docs::update::toc', this.readme.replace(/<h3.*?<\/h3>/g, '') || '');
        },

        beforeDestroy() {
            this.$root.$emit('bv-docs::update::toc', '');
        }
    };
</script>
