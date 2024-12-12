<template>
    <section class="title">

        <div class="background-layer"></div>
        <div class="header">
            <h1>{{ title }}</h1>
            <h3>{{ subtitle }}</h3>
        </div>

        <div class="authors-wrapper">
            <div v-for="(authorsItem, i) in authors" :key="i" class="authors">
                <span v-for="(author, j) in authorsItem" :key="j">
                    <sup v-if="author.prefix">{{ author.prefix }}</sup>
                    <a v-if="author.homepage" :href="author.homepage" target="_blank" class="author-name">{{ author.name }}</a>
                    <span v-else class="author-name">{{ author.name }}</span>
                    <sup v-if="author.suffix">{{ author.suffix }}</sup>
                    <span v-if="j < authorsItem.length - 1">&nbsp;&nbsp;&nbsp;&nbsp;</span>
                </span>
            </div>
        </div>

        <div class="resources">
            <a v-if="resources.pdf" class="button" :href="resources.pdf" target="_blank">
                <i class="iconfont icon-lm-pdf"></i>
                <span>Arxiv</span>
            </a>
            <a v-if="resources.github" class="button" :href="resources.github" target="_blank">
                <i class="iconfont icon-lm-github"></i>
                <span>Github</span>
            </a>
            <a v-if="resources.samples" class="button" :href="resources.samples" target="_blank">
                <i class="iconfont icon-lm-samples"></i>
                <span>View more samples</span>
            </a>
        </div>

        <!-- <video v-if="mainVideo" class="main-video" :src="mainVideo" muted loop controls></video> -->
    </section>
</template>


<script lang="ts" setup>
import { onMounted } from 'vue';

interface Props {
    title?: string;
    subtitle?: string;
    authors?: any[];
    resources?: any;
    mainVideo?: string;
    backgroundVideo?: string;
}
const { props } = defineProps<{ props: Props }>();

const title = props.title;
const subtitle = props.subtitle;
const authors = props.authors;
const resources = props.resources;
const mainVideo = (props.mainVideo || '').startsWith('assets')
    ? new URL(`../${props.mainVideo}`, import.meta.url).href
    : props.mainVideo;
// const backgroundVideo = props.backgroundVideo

onMounted(() => {
    if (title) {
        document.title = title;
    }
    if (subtitle) {
        document.title += `: ${subtitle}`;
    }
});
</script>

<style lang="scss" scoped>

.title {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    min-height: 100vh;
    justify-content: center;
    background-color: transparent;
    z-index: 1;
    margin-bottom: 1px;
    
    padding: 20px;

    .background-layer {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-image: url('http://cdn.aondata.work//OpenHumanVid/assets/videos/bottom.png'); // 替换为你的图片路径
        background-size: cover;
        background-position: center;
        z-index: -1; // 确保背景层在内容下面
    }
    /* 添加白色模糊层 */
    &::before {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(255, 255, 255, 0.8); /* 白色半透明 */
        filter: blur(1px); /* 模糊效果 */
        z-index: 0 ; /* 确保在内容与背景图片之间 */
        pointer-events: none; /* 防止影响交互 */
    }

    .header {
        margin-bottom: 20px;

        h1 {
            font-size: 7rem;
            margin: 2;
        }

        h3 {
            font-size: 2.5rem;
            margin: 2;
        }
        z-index: 1;

    }

    .authors-wrapper {
        margin: 15px 0;

        .authors {
            font-size: 1.8rem;

            .author-name {
                font-weight: 500;
            }
        }
        z-index: 1;

    }

    .resources {
        display: flex;
        justify-content: center;
        gap: 10px;
        margin: 20px 0;
        z-index: 1;

        .button {
            display: flex;
            align-items: center;
            background-color: #f0f0f0;
            border: 1px solid #ccc;
            padding: 10px 15px;
            text-decoration: none;
            color: #333;
            border-radius: 5px;
            transition: background-color 0.3s;

            &:hover {
                background-color: #e0e0e0;
            }

            i {
                margin-right: 8px;
            }
        }
    }

}
</style> 
  