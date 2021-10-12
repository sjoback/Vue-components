<template>
    <section
        class="section"
        :class="sectionPadding"
    >
        <div
            class="section-inner"
            :class="'section-width-' + width"
        >
            <slot></slot>
        </div>
    </section>
</template>

<script>
export default {
    props: {
        width: {
            type: String,
            required: false,
            default: 'sm'
        },
        label: {
            type: String,
            required: false
        }
    },
    computed: {
        sectionPadding() {
            if (this.label) {
                let padding = this.label;

                if (padding === 'no_padding') return 'n-p';

                if (padding === 'padding_bottom') return 'p-b';

                if (padding === 'padding_top') return 'p-t';
            }
        }
    }
}
</script>
