<template>
    <Section
        :background="slice.primary.background"
        width="md"
        class="banner banner-simple"
    >
        <div class="text text-center">
            <h1 class="section-header">{{$prismic.asText(slice.primary.h1)}}</h1>
            <p>{{$prismic.asText(slice.primary.teaser1)}}</p>
        </div>
    </Section>
</template>


<script>
export default {
    props: {
        slice: {
            type: Object,
            required: true
        }
    }
}
</script>
