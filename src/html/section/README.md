# Section

## Useage
Import the component
```
import { Section } from '@swegaming-ab/vue-components'
```

In your template
```
<Section
    width=""
    :label=""
>
    // content
</Section>
```

## Props
| Props            | Type     | Required   | Default   | Description                                   |
|:-----------------|:---------|:-----------|:----------|:----------------------------------------------|
| width            | String   | false      | sm        | Sets width for inner container                |
| label            | String   | false      | padding   | Sets section class based on slice_label       |
