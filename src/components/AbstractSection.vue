<template>
    <section class="abstract">
        <div>
            <h2>{{ title }}</h2>
            <div v-if="figure" class="figure">
                <img :src="figure">
            </div>
            <div v-if="video" class="figure">
                <video :src="video" />
            </div>
            <p>{{ props.content }}</p>
        </div>
    </section>
</template>

<script setup lang="ts">
interface Props {
    title?: string
    content?: string
    figure?: string
    video?: string
}
const { props } = defineProps<{ props: Props }>()
const title = props.title || "Abstract"
const figure = (props.figure || "").startsWith("assets") ? new URL(`../${props.figure}`, import.meta.url).href : props.figure
const video = (props.video || "").startsWith("assets") ? new URL(`../${props.video}`, import.meta.url).href : props.video

</script>

<style lang="scss" scoped>
.abstract {
    h2 {
        // font-family: 'Caveat', cursive;
        // font-size: 2.5rem;
        margin-top: 0px;
        margin-bottom: 70px;
    }
    div {
        max-width: 1400px;
        margin-top: 50px;
        @apply w-full mt-2;
    }

    li {
        @apply flex flex-row my-1;

        :first-child {
            @apply mr-2;
        }
    }
    .figure {
        margin-top: 10px;
        max-width: 1400px;
        margin: 1rem 0;
    }
}

.figure {
    max-width: 1200px;
    margin: 1rem 0;
}

p {
    white-space: pre-line;
}
</style>