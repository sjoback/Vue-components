# CookieConsent

## Useage
Import the component
```
import { CookieConsent } from '@swegaming-ab/vue-components'
```

In your template.
```
<client-only>
    <CookieConsent
        :content=""
        :buttonText=""
    />
</client-only>
```

## Props
| Props        | Type     | Required   |
|:-------------|:---------|:-----------|
| content      | String   | True       |
| buttonText   | String   | True       |

## Stylesheet boilerplate
Sass class-structure. Copy & paste!
```
.cookie-consent {
    &-content {}
    &-btn {}
}

```
