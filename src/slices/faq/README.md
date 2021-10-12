# FAQ

## Useage
Import the component
```
import { Ucr } from '@swegaming-ab/vue-components'
```

In your template.
```
<QuestionAnswer
    :question=""
    :answer=""
/>
```

## Props
| Props      | Type     | Required   |
|:-----------|:---------|:-----------|
| question   | String   | True       |
| answer     | String   | True       |

## Stylesheet boilerplate
Sass class-structure. Copy & paste!
```
.question-answer {
    .question {
        &-text {}
        &-icon {}
    }

    .answer {
        &-text {}
    }
}
```
