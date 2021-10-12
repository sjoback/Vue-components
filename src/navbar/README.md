# Navigation

In order for this navbar to function you will have to copy & paste the
prismic.json directly into prismic.

## Useage
Import the component
```
import { Navbar } from '@swegaming-ab/vue-components'
```

In your template
```
<Navbar
  :items=""
  home-link=""
  fav-icon=""
  :offset=""
  :breakpoint=""
  :nav-text=""
  :show-icons=""
/>
```

## Props
| Props           | Type     | Required   | Default               |
|:----------------|:---------|:-----------|:----------------------|
| items           | Array    | true       |                       |
| homeLink        | String   | false      | /                     |
| favIcon         | String   | false      |                       |
| offset          | Number   | false      | 600                   |
| breakpoint      | Number   | false      | 900                   |
| showIcons       | Boolean  | false      | false                 |
| navText         | String   | false      | false                 |



## Stylesheet boilerplate
Sass class-structure with prefixed values. Copy & paste!
```
.nav.scrolled {
    @media screen and (min-width: 900px) {
        animation: dropdown .15s;
    }
}

@keyframes dropdown {}

.nav {
    @media screen and (min-width: 900px) {}

    &-logo {
        img {}

        @media screen and (min-width: 900px) {
            img {}
        }
    }

    &-list {
        order: 1;
        z-index: 3;
        position: relative;

        @media screen and (min-width: 900px) {}

        &-item {
            display: none;
            position: relative;

            @media screen and (min-width: 900px) {
                display: flex;                
            }

            &__dropdown.show { display: flex!important; }
            &__dropdown {
                .ddm_text {
                    position: relative;
                    &:after {
                        position: relative;
                        right: 0;
                        padding-left: 10px;
                        font-family: Font Awesome\ 5 Free;
                        font-weight: 900;
                        content: "\f078";
                    }
                }

                .dropdown {

                    @media screen and (min-width: 900px) {
                        position: absolute;
                        top: 100%;
                    }

                    li {

                        a {

                            @media screen and (min-width: 900px) {}
                        }
                    }
                }
            }

            &__link {

            }
        }
    }

    &-toggle {

        @media screen and (min-width: 900px) {
            display: none;
        }

        &__btn {}
    }

    &-overlay {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        opacity: .6;
        z-index: 2;
    }
}
```
