<template>
    <div
        class="question-answer"
        itemscope
        itemprop="mainEntity"
        itemtype="https://schema.org/Question"
    >
        <div
            @click="toggle"
            class="question"
        >
            <span
                class="question-text"
                itemprop="name"
                v-html="question"
            />
            <span class="question-icon">
                <transition
                    name="spin"
                    mode="out-in"
                >
                    <i v-if="show" class="fas fa-chevron-up" />
                    <i v-else class="fas fa-chevron-down" />
                </transition>
            </span>
        </div>
        <div
            class="answer"
            itemscope itemprop="acceptedAnswer"
            itemtype="https://schema.org/Answer"
            :class="{active: show}"
        >
            <span
                class="answer-text"
                itemprop="text"
                v-html="answer"
            />
        </div>
    </div>
</template>
<script>
    export default {
        props: {
            question: {
                type: String,
                required: true
            },
            answer: {
                type: String,
                required: true
            }
        },
        data() {
            return {
                show: false
            }
        },
        methods: {
            toggle() {
                this.show = !this.show;
            }
        }
    }
</script>
<style lang="scss">
    .question-answer {
        display: flex;
        flex-wrap: wrap;

        .active { display: block!important; }

        .question {
            width: 100%;
            cursor: pointer;
            display: flex;
            justify-content: space-between;

            &-text {
                flex: 1;
            }
            &-icon {
                display: flex;
                justify-content: center;
                align-items: center;
            }
        }

        .answer {
            width: 100%;
            display: none;
        }

        .spin-enter-active {
            transition: all .25s ease-in-out;
        }

        .spin-leave-active {
            transition: all .25s ease-in-out;
        }

        .spin-enter, .spin-leave-to {
            transform: rotate(90deg);
            opacity: 0;
        }
    }
</style>
