<template>
    <!--
        NOTE: In order to animate image you have to locally declare the
        imageBlock directive and set animate prop to true
    -->
    <Section
        :background="background"
        :width="width"
        class="image-block"
    >
        <div class="image-block-img">
            <PrismicImage
                v-if="animate"
                v-imageBlock
                :img="image"
                class="br-5"
            />
            <PrismicImage
                v-else
                :img="image"
                class="br-5"
            />
        </div>
        <div
            v-html="$prismic.asHtml(text)"
            class="image-block-text"
        />
    </Section>
</template>
<script>
  export default {
      props: {
          animate: {
              type: Boolean,
              required: false,
              default: false
          },
          image: {
              type: Object,
              required: true
          },
          text: {
              type: Object,
              required: false
          },
          background: {
              type: String,
              required: false,
              default: 'white'
          },
          width: {
              type: String,
              required: false,
              default: 'sm'
          }
      }
  }
</script>
