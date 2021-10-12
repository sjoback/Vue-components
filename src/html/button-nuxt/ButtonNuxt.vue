<template>
    <nuxt-link
        class="btn btn-nuxt"
        :class="[
            'btn-' + background,
            'btn-' + size
        ]"
        :to="$prismic.linkResolver(link)"
    >
        <span class="btn-nuxt-text">{{text}}</span>
        <i
            v-if="icon"
            :class="icon"
            class="btn-nuxt-icon"
        ></i>
    </nuxt-link>
</template>
<script>
export default {
    props: {
        background: {
            type: String,
            default: 'transparent',
            required: false
        },
        size: {
            type: String,
            default: 'md',
            required: false
        },
        icon: {
            type: String,
            required: false,
        },
        link: {
            type: Object,
            required: true
        },
        text: {
            type: String,
            required: false,
            default: 'Click me'
        }
    }
}
</script>
