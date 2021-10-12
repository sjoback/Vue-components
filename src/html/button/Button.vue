<template>
    <button
        @click="$emit('click')"
        class="btn btn-btn"
        :class="[
            'btn-' + background,
            'btn-' + size
        ]"
        type="button"
        name="button"
    >
        <span class="btn-btn-text">{{text}}</span>
        <i
            v-if="icon"
            :class="icon"
            class="btn-btn-icon"
        ></i>
    </button>
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
        text: {
            type: String,
            required: false,
            default: 'Click me'
        }
    }
}
</script>
