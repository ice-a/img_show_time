<template>
  <div>
    <!-- 按钮用于重新加载图片 -->
    <a-button type="primary" @click="reload">展示时间</a-button>

    <!-- 图片展示区域 -->
    <div class="image-grid">
      <div v-for="(image, index) in images" :key="index" class="image-item">
        <div class="image-container">
          <img :src="image" alt="image" class="image" />
        </div>
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
  'https://t.alcy.cc/mp',
  'https://www.loliapi.com/acg',
  'https://www.dmoe.cc/random.php',
  'https://api.btstu.cn/sjbz/api.php',
  'https://t.alcy.cc/ys',
  'https://img.paulzzh.com/touhou/random',
  'https://t.alcy.cc/moez',
  'https://t.alcy.cc/ycy',
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
  gap: 10px; /* 图片之间的间距 */
}

.image-item {
  flex: 1 1 calc(25% - 10px); /* 每行显示4张图片，减去间距 */
  box-sizing: border-box;
}

.image-container {
  position: relative;
  width: 100%;
  padding-top: 100%; /* 1:1 宽高比 */
  overflow: hidden;
  border-radius: 8px;
}

.image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover; /* 保持图片比例 */
}

/* 响应式布局 */
@media (max-width: 768px) {
  .image-item {
    flex: 1 1 calc(50% - 10px); /* 在小屏幕上每行显示2张图片 */
  }
}

@media (max-width: 480px) {
  .image-item {
    flex: 1 1 100%; /* 在超小屏幕上每行显示1张图片 */
  }
}
</style>