<template>
    <nav class="nav">
        <div class="nav-logo">
            <nuxt-link :to="navbarHomeLink">
                <img
                    :src="favIcon"
                    alt="favicon"
                />
                <div
                    v-html="navbarText"
                    class="nav-text"
                />
            </nuxt-link>
        </div>

        <ul
            :class="{show: showNavList}"
            class="nav-list"
        >
            <li
                v-for="(item, index) in navItems"
                :key="index"
                @mouseenter="mouseEnter(item, index)"
                @click="mouseClick(item, index)"
                @mouseleave="mouseLeave(item, index)"
            >
                <div
                    class="nav-list-item"
                    :class="{active: showDropdown === index}"
                    v-if="item.primary.ddm_text"
                >
                    {{ item.primary.ddm_text }}
                </div>

                <nuxt-link
                    v-else
                    :to="$prismic.linkResolver(item.primary.sl_link)"
                    class="nav-list-item"
                >
                    {{ item.primary.sl_text }}
                </nuxt-link>

                <transition name="nav">
                <div
                    v-show="showDropdown === index"
                    class="dropdown"
                    v-if="item.primary.ddm_text"
                >
                    <ul>
                        <li
                            v-for="(link, index) in item.items"
                            :key="index"
                        >
                            <nuxt-link
                                class="ddm_link"
                                :to="$prismic.linkResolver(link.ddm_link)"
                            >
                                <PrismicImage
                                    v-if="link.ddm_link && link.ddm_link.data && link.ddm_link.data.icon"
                                    :img="link.ddm_link.data.icon"
                                    w="50"
                                    h="50"
                                />
                                <span class="ddm_link_text">{{link.ddm_link_text}}</span>
                            </nuxt-link>
                        </li>
                    </ul>
                </div>
                </transition>
            </li>
        </ul>

        <div class="nav-slot">
            <slot></slot>
        </div>

        <div class="nav-toggle">
            <i
                class="nav-toggle__btn"
                @click="showNavList =! showNavList, showDropdown =! showDropdown"
                :class="[ mobileMenuIconOpen, { open: showNavList } ]"
            />
        </div>
    </nav>
</template>
<script>
export default {
    props: {
        favIcon: {
            type: String,
            required: false,
            default: '@/static/favicon.png'
        },
        mobileMenuIconOpen: {
            type: String,
            required: false,
            default: 'fas fa-bars'
        },
        mobileMenuIconClose: {
            type: String,
            required: false,
            default: 'fas fa-times'
        },
        navbarHomeLink: {
            type: String,
            required: false,
            default: '/'
        },
        navbarText: {
            type: String,
            required: false
        },
        dropdownMenuIcon: {
            type: String,
            required: false
        },
        navItems: {
            type: Array,
            required: true
        }
    },
    data() {
        return {
            showDropdown: false,
            showNavList: false
        }
    },
    watch: {
        '$route'() {
            this.showDropdown = undefined
            this.showNavList = undefined
        }
    },
    methods: {
        mouseClick(link, index) {
            if(window.innerWidth < 900) {
                if(link.primary.ddm_text && this.showDropdown !== index) this.showDropdown = index
                else this.showDropdown = false
            }
        },
        mouseEnter(link, index) {
            if(link.primary.ddm_text && window.innerWidth > 900) this.showDropdown = index
        },
        mouseLeave(link, index) {
            if(link.primary.ddm_text && window.innerWidth > 900) this.showDropdown = undefined
        }
    }
}
</script>
