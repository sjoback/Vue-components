# Navigation

In order for this navbar to function you will have to copy & paste the
prismic.json directly into prismic.

## Useage
Import the component  

```
import { Navbar } from '@leetajz/vue-components'
```

In your template

```
<Navbar
    navbarText=""
    :navItems=""
    mobileMenuIconOpen=""
    mobileMenuIconClose=""
    navbarHomeLink=""
    dropdownMenuIcon=""
    favIcon=""
/>
```

## Props
| Props                 | Type     | Required   | Default               |
|:----------------------|:---------|:-----------|:----------------------|
| navbarText            | String   | false      |                       |
| navItems              | Array    | true       |                       |
| mobileMenuIconOpen    | String   | false      | fas fa-bars           |
| mobileMenuIconClose   | String   | false      | fas fa-times          |
| navbarHomeLink        | String   | false      | /                     |
| dropdownMenuIcon      | String   | false      |                       |
| favIcon               | String   | false      | @/static/favicon.png  |


## Stylesheet boilerplate
Sass class-structure. Copy & paste!
```
.nav {

    &-logo {
        .toggle {}

        img {}

        i {}

        @media screen and (min-width: 900px) {
            i {}
        }
    }

    &-list.show {
        @media screen and (min-width: 900px) {}
    }
    &-list {
        @media screen and (min-width: 900px) {}

        li {
            i {}

            .nav-list-item {}

            .nav-list-item.active {}

            @media screen and (min-width: 900px) {}

            .dropdown {
                ul {
                    li {
                        a {
                            img {}
                        }
                    }
                }

                @media screen and (min-width: 900px) {
                    ul {
                        li {}
                    }
                }
            }
        }
    }

    @media screen and (max-width: $desktop) {
        .nav-enter-active, .nav-leave-active {}
        .nav-enter, .nav-leave-to {
    }

    .menuToggle-enter-active, .menuToggle-leave-active {}
    .menuToggle-enter, .menuToggle-leave-to {}
}

```
