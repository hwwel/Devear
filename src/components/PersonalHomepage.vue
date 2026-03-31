<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { LinkOutlined } from '@ant-design/icons-vue'

const poems = [
  '海内存知己，天涯若比邻',
  '长风破浪会有时，直挂云帆济沧海',
  '山重水复疑无路，柳暗花明又一村',
  '欲穷千里目，更上一层楼',
  '会当凌绝顶，一览众山小',
  '路漫漫其修远兮，吾将上下而求索',
  '天生我材必有用，千金散尽还复来',
  '采菊东篱下，悠然见南山',
  '大鹏一日同风起，扶摇直上九万里',
  '不飞则已，一飞冲天；不鸣则已，一鸣惊人',
  '宝剑锋从磨砺出，梅花香自苦寒来',
  '千磨万击还坚劲，任尔东西南北风'
]

const currentPoem = ref('')
const avatarUrl = ref('https://q1.qlogo.cn/g?b=qq&nk=3626444959&s=640')
const name = ref('Devear')
const showContent = ref(false)

const getRandomPoem = () => {
  const randomIndex = Math.floor(Math.random() * poems.length)
  return poems[randomIndex]
}

const refreshPoem = () => {
  let newPoem
  do {
    newPoem = getRandomPoem()
  } while (newPoem === currentPoem.value)
  currentPoem.value = newPoem
}

onMounted(() => {
  currentPoem.value = getRandomPoem()
  setTimeout(() => {
    showContent.value = true
  }, 100)
})
</script>

<template>
  <div class="homepage-container">
    <div class="background-shapes">
      <div class="shape shape-1"></div>
      <div class="shape shape-2"></div>
      <div class="shape shape-3"></div>
      <div class="shape shape-4"></div>
    </div>

    <div class="content-wrapper" :class="{ 'show': showContent }">
      <div class="avatar-section">
        <div class="avatar-container">
          <img 
            :src="avatarUrl" 
            alt="Avatar" 
            class="avatar"
          />
          <div class="avatar-ring"></div>
        </div>
      </div>

      <div class="info-section">
        <h1 class="name">{{ name }}</h1>
        <div class="divider"></div>
        <div class="poem-container">
          <p class="poem">{{ currentPoem }}</p>
          <a-button 
            type="text" 
            class="refresh-btn"
            @click="refreshPoem"
          >
            <template #icon>
              <LinkOutlined />
            </template>
            换一句
          </a-button>
        </div>
      </div>

      <div class="footer">
        <p class="footer-text">© 2024 {{ name }}. All rights reserved.</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.homepage-container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  overflow: hidden;
}

.background-shapes {
  position: absolute;
  width: 100%;
  height: 100%;
  overflow: hidden;
  z-index: 0;
}

.shape {
  position: absolute;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.1);
  animation: float 6s ease-in-out infinite;
}

.shape-1 {
  width: 300px;
  height: 300px;
  top: -100px;
  left: -100px;
  animation-delay: 0s;
}

.shape-2 {
  width: 200px;
  height: 200px;
  top: 20%;
  right: -50px;
  animation-delay: 2s;
}

.shape-3 {
  width: 250px;
  height: 250px;
  bottom: -80px;
  left: 10%;
  animation-delay: 4s;
}

.shape-4 {
  width: 180px;
  height: 180px;
  bottom: 30%;
  right: 20%;
  animation-delay: 1s;
}

.content-wrapper {
  text-align: center;
  padding: 60px 40px;
  background: rgba(255, 255, 255, 0.95);
  border-radius: 24px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
  max-width: 500px;
  width: 90%;
  z-index: 1;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}

.content-wrapper.show {
  opacity: 1;
  transform: translateY(0);
}

.avatar-section {
  margin-bottom: 30px;
}

.avatar-container {
  position: relative;
  width: 150px;
  height: 150px;
  margin: 0 auto;
}

.avatar {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  object-fit: cover;
  border: 4px solid #fff;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.2);
  animation: scaleIn 0.8s ease-out;
}

.avatar-ring {
  position: absolute;
  top: -8px;
  left: -8px;
  right: -8px;
  bottom: -8px;
  border-radius: 50%;
  border: 3px solid #667eea;
  animation: pulse 2s infinite;
}

.info-section {
  margin-bottom: 40px;
}

.name {
  font-size: 36px;
  font-weight: 700;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin-bottom: 16px;
  animation: fadeInUp 0.8s ease-out 0.2s both;
}

.divider {
  width: 60px;
  height: 4px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  margin: 0 auto 24px;
  border-radius: 2px;
  animation: fadeIn 0.8s ease-out 0.4s both;
}

.poem-container {
  animation: fadeInUp 0.8s ease-out 0.6s both;
}

.poem {
  font-size: 18px;
  color: #333;
  font-weight: 500;
  line-height: 1.6;
  margin-bottom: 16px;
  font-style: italic;
}

.refresh-btn {
  color: #667eea;
  font-size: 14px;
  transition: all 0.3s ease;
}

.refresh-btn:hover {
  color: #764ba2;
  transform: scale(1.05);
}

.footer {
  animation: fadeIn 0.8s ease-out 1s both;
}

.footer-text {
  color: #999;
  font-size: 14px;
  margin: 0;
}

@media (max-width: 768px) {
  .content-wrapper {
    padding: 40px 30px;
    max-width: 90%;
  }

  .avatar-container {
    width: 120px;
    height: 120px;
  }

  .avatar {
    width: 120px;
    height: 120px;
  }

  .name {
    font-size: 28px;
  }

  .poem {
    font-size: 16px;
  }
}
</style>
