<template>
    <section>
      <h2 class="video-title">{{ title }}</h2>
      <div class="video-grid">
        <div v-for="(video, index) in items" :key="index" class="video-item">
          <div class="caption" v-if="captions[index]">
            <span>{{ captions[index] }}</span>
          </div>
          <video
            :src="video"
            autoplay
            muted
            loop
            preload="metadata"
            class="video-player"
          ></video>
        </div>
      </div>
    </section>
  </template>
  

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Caveat:wght@400;700&display=swap');

h2 {
  margin-top: 10px;
  text-align: center; /* 居中标题 */
  margin-bottom: 45px; /* 减小与视频网格的间距 */
  /* font-weight: 700; 增加字体权重以使标题更突出 */
  /* font-family: ; */
  color: #333; /* 标题颜色可选 */
}

.video-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr); /* 一行四个视频，均分宽度 */
  gap: 0; /* 去掉间距 */
  width: 100vw; /* 确保整个容器占满屏幕宽度 */
  margin-bottom: 0px;
}

.video-item {
  position: relative;
  overflow: hidden;
  width: 100%; /* 确保每个格子占满分配宽度 */
  
}

.video-player {
  width: 100%; /* 视频宽度占满容器 */
  height: auto; /* 高度根据宽度自动调整 */
  display: block;
  pointer-events: none;
  
}

.caption {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(255, 255, 255, 0.2);
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
  font-size: 24px;
  font-weight: 700;
  font-family: 'Caveat', cursive;
  text-align: center;
  pointer-events: none;
}
</style>



<script setup lang="ts">
interface Props {
  id?: string;
  title?: string;
  items?: string[];
  captions?: string[];
  annotations?: { [key: string]: { clip_id: string; method: string; feature: any } }[];
}

const { props } = defineProps<{ props: Props }>();

const title = props.title || '';
const items = (props.items || []).map((sub) =>
  sub.startsWith('assets') ? new URL(`../${sub}`, import.meta.url).href : sub
);
const annotations = props.annotations || [];
const captions = annotations.map((v) => v['Captions']?.feature['short_caption']);

function hideCaption(evt: MouseEvent) {
  const containerEle = evt.target as HTMLElement;
  const element: HTMLElement = containerEle.querySelector('.caption')!;
  if (element) {
    element.style.display = 'none';
  }
}

function showCaption(evt: MouseEvent) {
  const containerEle = evt.target as HTMLElement;
  const element: HTMLElement = containerEle.querySelector('.caption')!;
  if (element) {
    element.style.display = 'flex';
  }
}
</script>
