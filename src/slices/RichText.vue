<template>
    <Section
        :width="width"
        :background="'bg-' + background"
        class="rich-text"
    >
        <div v-html="$prismic.asHtml(content)"></div>
    </Section>
</template>
<script>
export default {
    props: {
        content: {
            type: Array,
            required: true
        },
        width: {
            type: String,
            required: false,
            default: 'sm'
        },
        background: {
            type: String,
            required: false,
            default: 'white'
        }
    }
}
</script>
