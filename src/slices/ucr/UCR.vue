<template>
    <Section
        class="ucr"
        width="sm"
        id="ucr"
    >
        <ul class="ucr-list">
            <li
                v-for="(rating, index) in ratings"
                :key="index"
                class="ucr-list-item"
            >
                <div class="rating-name">{{ rating.rater_name }}</div>

                <div class="rating-stars">
                    <i
                        v-for="i in 5"
                        :key="i"
                        :class="{ active: i <= rating.rating_score }"
                        class="fas fa-star"
                    />
                </div>
                <div class="rating-header">{{ rating.rating_header }}</div>
                <div class="rating-body" v-html="getRatingBodyHtml(rating.rating_body)"></div>
                <div class="rating-timestamp">{{ postedAt( rating.posted_at ) }}</div>
            </li>
        </ul>

        <form id="form" class="ucr-form" v-if="!postSuccess">
            <h2 class="ucr-form-title">{{ formTitle }}</h2>

            <div class="ucr-form-input-container">
                <label for="score" v-html="labelScore" />
                <div class="stars">
                    <i @click="newRating.rating_score = 1" @mouseenter="ratingScoreHover = 1" @mouseleave="ratingScoreHover = undefined" :class="[{ratingSet: newRating.rating_score}, {hover: ratingScoreHover}]" class="fas fa-star" />
                    <i @click="newRating.rating_score = 2" @mouseenter="ratingScoreHover = 2" @mouseleave="ratingScoreHover = undefined" :class="[{ratingSet: newRating.rating_score > 1}, {hover: ratingScoreHover > 1}]" class="fas fa-star" />
                    <i @click="newRating.rating_score = 3" @mouseenter="ratingScoreHover = 3" @mouseleave="ratingScoreHover = undefined" :class="[{ratingSet: newRating.rating_score > 2}, {hover: ratingScoreHover > 2}]" class="fas fa-star" />
                    <i @click="newRating.rating_score = 4" @mouseenter="ratingScoreHover = 4" @mouseleave="ratingScoreHover = undefined" :class="[{ratingSet: newRating.rating_score > 3}, {hover: ratingScoreHover > 3}]" class="fas fa-star" />
                    <i @click="newRating.rating_score = 5" @mouseenter="ratingScoreHover = 5" @mouseleave="ratingScoreHover = undefined" :class="[{ratingSet: newRating.rating_score > 4}, {hover: ratingScoreHover > 4}]" class="fas fa-star" />
                </div>
            </div>

            <div class="ucr-form-input-container">
                <label for="name" v-html="labelName" />
                <input name="name" type="text" v-model="newRating.rater_name" />
            </div>

            <div class="ucr-form-input-container">
                <label for="email" v-html="labelEmail" />
                <input name="email" type="text" v-model="newRating.rater_email" />
                <div class="error" v-if="postError.rater_email">
                    {{ emailErrorMsg }}
                </div>
            </div>

            <div class="ucr-form-input-container" v-if="enableHeaderInput">
                <label for="header" v-html="labelHeader" />
                <input name="header" type="text" v-model="newRating.rating_header" />
            </div>

            <div class="ucr-form-input-container">
                <label for="body" v-html="labelBody" />
                <textarea name="body" v-model="newRating.rating_body" rows="5" cols="80" />
            </div>

            <div class="ucr-form-submit-button">
                <button
                    type="submit"
                    @click="submit"
                    :class="{ disabled: !enableSubmit }"
                >
                    {{ submitButtonText }}
                </button>
            </div>
        </form>

        <div id="form" v-html="postSuccessMsg" class="ucr-form width-full post-success" v-else />
    </Section>
</template>

<script>
import axios from 'axios'
import { orderBy } from 'lodash'
export default {
    props: {
        coreId: {
            type: Number,
            required: true
        },
        coreRatings: {
            type: Object,
            required: true
        },
        formTitle: {
            type: String,
            required: false
        },

        labelScore: {
            type: String,
            required: false
        },
        labelName: {
            type: String,
            required: false
        },
        labelEmail: {
            type: String,
            required: false
        },
        labelHeader: {
            type: String,
            required: false
        },
        labelBody: {
            type: String,
            required: false
        },

        submitButtonText: {
            type: String,
            required: false,
            default: 'Submit'
        },

        enableHeaderInput: {
            type: Boolean,
            default: true
        },

        formSourceId: {
            type: Number,
            required: true
        },
        postSuccessMsg: {
            type: String,
            required: true
        },
        emailErrorMsg: {
            type: String,
            required: true
        }
    },
    data () {
        return {
            newRating: {
                source_id: undefined,
                brand_id: undefined,
                rating_header: undefined,
                rating_body: '',
                rating_score: undefined,
                rater_name: undefined,
                rater_email: undefined
            },
            enableSubmit: false,
            ratingScoreHover: undefined,
            posting: false,
            postSuccess: false,
            postError: false
        }
    },
    computed: {
        ratings () {
            return orderBy(this.coreRatings.data, 'posted_at', 'desc')
        }
    },
    watch: {
        newRating: {
            deep: true,
            handler() {
                if(
                    this.newRating.rating_score &&
                    this.newRating.rater_name &&
                    this.newRating.rater_email &&
                    this.newRating.rating_body.length >= 20
                ) {
                    this.enableSubmit = true
                }
                else {
                    this.enableSubmit = false
                }
            }
        }
    },
    methods: {
        submit() {
            this.posting = true;
            this.postError = []

            this.newRating.brand_id = this.coreId;
            this.newRating.source_id = this.formSourceId;

            var url = 'https://api.core.compary.com/api/v0/ratings';

            axios.post( url, this.newRating ).then( ( res ) => {
                this.posting = false;
                this.postSuccess = true;
            })
            .catch( ( e ) => {
                this.postError = e.response.data.error;
                this.posting = false;
            })
        },

        postedAt( string ) {
            var format = string.split("T")
            return format[0]
        },

        getRatingBodyHtml(ratingBody) {
            let html = '';
            ratingBody
                .split('\n')
                .filter(e => e.length > 0)
                .forEach(element => {
                    html += `<p>${element}</p>`;
                });

            return html;
        }
    }
}
</script>
