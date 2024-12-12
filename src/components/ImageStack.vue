<template>
    <section class="image-stack">
      <h2>{{ title }}</h2>
      <div>
        <img
          v-for="(image, index) in images"
          :key="index"
          :src="image"
          :alt="'Image ' + (index + 1)"
        />
      </div>
    </section>
</template>

<script setup lang="ts">

interface Props {
title?: string
imageList?: string[]
}

const {props} = defineProps<{props: Props}>()

// Provide default values for props
const title = props.title || "Stacked Images"
const images = props.imageList || []

</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Caveat:wght@400;700&display=swap');


h2 {
    // font-family: 'Caveat', cursive;
    margin-top: 0px; /* 减小与视频网格的间距 */
    margin-bottom: 0px; /* 减小与视频网格的间距 */
}

.image-stack {
    div {
        max-width: 1400px;
        @apply w-full mt-2;
    }
}

img {
    margin: 2rem 0;
}

</style>