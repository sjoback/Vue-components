<template>
    <nav
        class="nav"
        :class="{ scrolled: scrolled }"
    >

        <div class="nav-logo">
            <nuxt-link :to="homeLink">
                <img
                    :src="favIcon"
                    alt="favicon"
                    loading="eager"
                    class="nav-logo__image"
                />
                <div class="nav-logo__text" v-html="navText"></div>
            </nuxt-link>
        </div>

        <ul class="nav-list">
            <li
                v-for="(item, index) in items"
                :key="`item${index}`"
                class="nav-list-item"
            >
                <div
                    class="nav-list-item__dropdown"
                    v-if="item.slice_type === 'dropdown_menu' || item.slice_type === 'dropdown'"
                    @mouseenter="onHover(index)"
                    @mouseleave="onHover(index)"
                    @click="onClick(index)"
                    :class="[{show: mobile}, {active: index === showDropdown}]"
                >
                    <span class="ddm_text">{{item.primary.ddm_text}}</span>

                    <ul
                        v-show="index === showDropdown"
                        class="dropdown"
                    >
                        <li
                            v-for="(link, linkIndex) in item.items"
                            :key="`linkDropdown${linkIndex}`"
                        >
                            <nuxt-link :to="$prismic.linkResolver(link.ddm_link)">
                                <PrismicImage
                                    v-if="link.ddm_link.data"
                                    :img="link.ddm_link.data.icon"
                                    :alt="link.ddm_link_text"
                                    w="50"
                                    h="50"
                                />
                                <span>{{ link.ddm_link_text }}</span>
                            </nuxt-link>
                        </li>
                    </ul>
                </div>

                <nuxt-link
                    v-else
                    :key="`link${index}`"
                    :to="$prismic.linkResolver(item.primary.sl_link)"
                    :class="[{show: mobile}, {active: index === showDropdown}]"
                    class="nav-list-item__link"
                >
                    {{ item.primary.sl_text }}
                </nuxt-link>
            </li>
        </ul>

        <div class="nav-slot">
            <slot></slot>
        </div>

        <div class="nav-toggle">
            <i
                class="nav-toggle__btn"
                @click="mobile =! mobile, showDropdown =! showDropdown"
                :class="{open: mobile}"
            />
        </div>

        <div
            @click="mobile = false, showDropdown = undefined"
            v-if="mobile"
            class="nav-overlay"
        />
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
        homeLink: {
            type: String,
            required: false,
            default: '/'
        },
        navText: {
            type: String,
            required: false
        },
        items: {
            type: Array,
            required: true
        },
        offset: {
            type: Number,
            required: false,
            default: 600
        },
        breakpoint: {
            type: Number,
            required: false,
            default: 900
        }
    },
    data() {
        return {
            mobile: false,
            showDropdown: undefined,
            scrolled: false
        }
    },
    watch: {
        mobile() {
            document.body.style.overflow = this.mobile ? 'hidden' : ''
        },
        '$route'() {
            this.mobile = false;
        }
    },
    methods: {
        onClick(index) {
            if(window.innerWidth < this.breakpoint) {
                if(this.showDropdown == index) {
                    this.showDropdown = undefined
                } else {
                    this.showDropdown = index;
                }
            }
        },

        onHover(index) {
            if(window.innerWidth > this.breakpoint) {
                if(this.showDropdown == index) {
                    this.showDropdown = undefined
                } else {
                    this.showDropdown = index;
                }
            }
        },

        onScroll(e) {
            if ( window.scrollY > this.offset ) this.scrolled = true
            else this.scrolled = false
        }
    },
    mounted() {
        window.addEventListener("scroll", this.onScroll)
    },
    beforeDestroy() {
        window.removeEventListener("scroll", this.onScroll)
    },
    beforeMount() {
        document.body.style.overflow = 'visible'
    }
}
</script>
