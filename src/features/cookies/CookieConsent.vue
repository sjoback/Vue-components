<template>
    <div
        class="cookie-consent"
        v-if="this.open"
    >
        <div class="cookie-consent-content" v-html="content"></div>

        <button
            class="cookie-consent-btn"
            @click="open = false"
        >
            {{ buttonText}}
        </button>
    </div>
</template>
<script>
export default {
    props: {
        content: {
            type: String,
            required: true
        },
        buttonText: {
            type: String,
            required: false,
            default: 'OK'
        }
    },
    data() {
        return {
            open: false
        }
    },
    methods: {
        isQuotaExceeded(e) {
            var quotaExceeded = false;
            if (e) {
                if (e.code) {
                    switch (e.code) {
                        case 22:
                        quotaExceeded = true;
                        break;
                        case 1014:
                        // Firefox
                        if (e.name === 'NS_ERROR_DOM_QUOTA_REACHED') {
                            quotaExceeded = true;
                        }
                        break;
                    }
                } else if (e.number === -2147024882) {
                    // Internet Explorer 8
                    quotaExceeded = true;
                }
            }
            return quotaExceeded;
        }
    },
    created() {
        if(!localStorage.getItem('cookie.consent.viewed')) {
            try {
                localStorage.setItem('cookie.consent.viewed', true);
                this.open = true;
            } catch(e) {
                if (this.isQuotaExceeded(e)) {
                    // Storage full, maybe notify user or do some clean-up
                }
            }
        }
    }
}
</script>
