<template>
  <div>
    <!-- 按钮用于重新加载图片 -->
    <a-button type="primary" @click="reload">展示时间</a-button>

    <!-- 图片展示区域 -->
    <div class="image-grid">
      <div v-for="(image, index) in images" :key="index" class="image-item">
        <img :src="image" alt="image" class="image" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// 图片数据
const images = ref([]);

// 定义多个图片 API
const imageApis = [
  'https://3650000.xyz/api/?type=img',
  'https://www.loliapi.com/acg',
  'https://www.dmoe.cc/random.php',
  'https://api.btstu.cn/sjbz/api.php',
  'https://t.alcy.cc/ys',
  "https://img.paulzzh.com/touhou/random",
  "https://t.alcy.cc/moez",
  "https://t.alcy.cc/ycy",


];

// 重新加载图片
const reload = () => {
  // 直接使用 API 的 URL 作为图片地址
  images.value = imageApis.map((api) => {
    // 添加时间戳参数，避免浏览器缓存
    return `${api}?timestamp=${new Date().getTime()}`;
  });
};

// 初始化时加载图片
reload();
</script>

<style scoped>
.image-grid {
  display: flex;
  flex-wrap: wrap;
  margin-top: 20px;
}

.image-item {
  width: 25%; /* 每行展示4个图片 */
  padding: 10px;
  box-sizing: border-box;
}

.image {
  width: 100%;
  height: 640px; /* 固定高度 */
  object-fit: cover; /* 保持图片比例 */
  border-radius: 8px;
}
</style>