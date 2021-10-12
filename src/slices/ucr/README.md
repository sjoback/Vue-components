# UCR

## Useage
Import the component
```
import { Ucr } from '@leetajz/vue-components'
```

In your template
```
<Ucr
    :coreId=""
    :coreRatings=""
    :formTitle=""
    :labelScore=""
    :labelName=""
    :labelEmail=""
    :labelHeader=""
    :labelBody=""
    :submitButtonText=""
    :postSuccessMsg=""
    :emailErrorMsg=""
    :enableHeaderInput=""
    :formSourceId=""
/>
```

## Props
| Props               | Type      | Required  | Description                            |
|:--------------------|:----------|:----------|:---------------------------------------|
| coreId              | Integer   | true      | The id in the Core                     |
| coreRatings         | Object    | true      | The object from the core export        |
| formTitle           | String    | true      | Form Title                             |
| labelScore          | String    | true      | Input label. Recieves html/string      |
| labelName           | String    | true      | Input label. Recieves html/string      |
| labelEmail          | String    | true      | Input label. Recieves html/string      |
| labelHeader         | String    | true      | Input label. Recieves html/string      |
| labelBody           | String    | true      | Input label. Recieves html/string      |
| submitButtonText    | String    | true      | Button text                            |
| postSuccessMsg      | String    | true      | Message shown on successful post       |
| emailErrorMsg       | String    | true      | Error message for faulty email input   |
| enableHeaderInput   | Boolean   | true      | Enable/Disable header input field      |
| formSourceId        | Number    | true      | Project specific id                    |


## Stylesheet boilerplate
Sass class-structure. Copy & paste!
```
.ucr {
    &-list {
        &-item {
            .rating-name {}
            .rating-stars {
                .active {
                    // sets color for user rating
                }
            }
            .rating-timestamp {}
            .rating-header {}
            .rating-body {}
        }
    }

    &-form {
        &-title {}
        &-input-container {
            label {}
            input {}
            textarea {}
            .stars {
                .active {
                    // sets color of chosen score stars
                }
            }
            .error {
                // container for displaying post error msg
            }
        }

        &-submit-button {
            button {}
            button.disabled {
                // disables button
                opacity: .6;
                pointer-events: none;
            }
        }
    }

    .post-success {
        h1,h2,h3,h4,h5,h6 {}
    }
}
```
