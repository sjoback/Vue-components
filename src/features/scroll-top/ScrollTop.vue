<template>
    <transition name="scroll-top">
        <div
            v-if="show"
            class="scroll-top"
            @click="toTop()"
        >
            <i class="fas fa-arrow-up"></i>
        </div>
    </transition>
</template>
<script>
    export default {
        data() {
            return {
                show: false
            }
        },
        methods: {
            scroll: function(){
                if(window.scrollY >= 300) this.show = true;
                else this.show = false;
            },
            toTop: function(){
                window.scrollTo({
                    top: 0,
                    left: 0,
                    behavior: 'smooth'
                })
            }
        },
        beforeDestroy() {
            window.removeEventListener('scroll', this.scroll);
        },
        mounted() {
            this.scroll();
            window.addEventListener('scroll', this.scroll);
        }
    }
</script>
