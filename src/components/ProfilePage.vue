<script setup>
// 导入需要的Vue功能
import { ref, onMounted } from 'vue';
// 导入图片资源
import profilePhoto from '../assets/suheng1.jpg';
import qqQRCode from '../assets/QQ.jpg';
import weixinQRCode from '../assets/weixin.jpg';
import qqIcon from '../assets/QQ.png';
import weixinIcon from '../assets/weixin.png';

// 个人信息数据
const personalInfo = ref({
  name: '苏恒',
  title: '河南科技大学男大一枚',
  description: '河南科技大学软件工程专业在校高材生，精通各种编程语言,喜爱各种丝的小姐姐！'
});

// 个人事迹数据
const achievements = ref([
  {
    id: 1,
    year: '2025',
    title: '319造粪机',
    description: '因其每天多次造粪，且造粪后产生巨大气味，被同学们亲切的称为319造粪机！'
  },
  {
    id: 2,
    year: '2025',
    title: '驾校风波后续',
    description: '科目二的第五次机会，背水一战通过科目二，并在接下来的科目三中一次过关！！！'
  },
  {
    id: 3,
    year: '2024',
    title: '驾校风波',
    description: '在科目二的考试中曾经遭遇四连败'
  },
  {
    id: 4,
    year: '2023',
    title: '加入河南科技大学',
    description: '高考以优异的成绩考入河南科技大学软件工程专业，开始了自己的大学生活。'
  }
]);

// 社交媒体链接
const socialLinks = ref([
  { id: 1, name: 'QQ', icon: 'src', url: '#', qrcode: qqQRCode },
  { id: 2, name: '微信', icon: '📱', url: '#', qrcode: weixinQRCode }
]);

// 添加二维码显示状态控制
const showQRCode = ref(null);

// 处理二维码显示
const handleQRCode = (type) => {
  showQRCode.value = showQRCode.value === type ? null : type;
};

// 技能列表
const skills = ref([
  { id: 1, name: '金铲铲之战', level: 95 },
  { id: 2, name: 'CSGO', level: 85 },
  { id: 3, name: '王者荣耀', level: 80 },
  { id: 4, name: '无畏契约', level: 65 }
]);

// 动画相关
const photoVisible = ref(false);
const infoVisible = ref(false);
const achievementsVisible = ref(false);

// 页面加载时的动画效果
onMounted(() => {
  setTimeout(() => {
    photoVisible.value = true;
  }, 300);
  
  setTimeout(() => {
    infoVisible.value = true;
  }, 800);
  
  setTimeout(() => {
    achievementsVisible.value = true;
  }, 1300);
});
</script>

<template>
  <div class="profile-container">
    <!-- 第一部分：照片 -->
    <section class="photo-section" :class="{ 'visible': photoVisible }">
      <div class="photo-container">
        <!-- 左侧QQ -->
        <div class="social-icon left">
          <div class="icon-wrapper" @click="handleQRCode('qq')">
            <img :src="qqIcon" alt="QQ图标" class="icon-image" />
            <div class="qrcode-container" :class="{ 'show': showQRCode === 'qq' }">
              <img :src="qqQRCode" alt="QQ二维码" class="qrcode-image" />
            </div>
          </div>
        </div>

        <!-- 中间照片 -->
        <div class="photo-wrapper">
          <img :src="profilePhoto" alt="个人照片" class="profile-photo" />
        </div>

        <!-- 右侧微信 -->
        <div class="social-icon right">
          <div class="icon-wrapper" @click="handleQRCode('weixin')">
            <img :src="weixinIcon" alt="微信图标" class="icon-image" />
            <div class="qrcode-container" :class="{ 'show': showQRCode === 'weixin' }">
              <img :src="weixinQRCode" alt="微信二维码" class="qrcode-image" />
            </div>
          </div>
        </div>
      </div>
    </section>
    
    <!-- 第二部分：个人简介 -->
    <section class="info-section" :class="{ 'visible': infoVisible }">
      <h1 class="name">{{ personalInfo.name }}</h1>
      <h2 class="title">{{ personalInfo.title }}</h2>
      <div class="divider"></div>
      <p class="description">{{ personalInfo.description }}</p>
      
      <!-- 技能展示部分 -->
      <div class="skills-container">
        <h3 class="skills-title">游戏技能</h3>
        <div class="skill" v-for="skill in skills" :key="skill.id">
          <div class="skill-header">
            <span class="skill-name">{{ skill.name }}</span>
            <span class="skill-level">{{ skill.level }}%</span>
          </div>
          <div class="skill-bar">
            <div class="skill-progress" :style="{ width: skill.level + '%' }"></div>
          </div>
        </div>
      </div>
    </section>
    
    <!-- 第三部分：个人事迹 -->
    <section class="achievements-section" :class="{ 'visible': achievementsVisible }">
      <h2 class="section-title">个人事迹</h2>
      <div class="timeline-container">
        <div class="timeline-line"></div>
        <div v-for="(achievement, index) in achievements" :key="achievement.id" 
             class="achievement-card" 
             :class="{ 'right': index % 2 === 0, 'left': index % 2 !== 0 }">
          <div class="achievement-dot"></div>
          <div class="achievement-year">{{ achievement.year }}</div>
          <div class="achievement-content">
            <h3 class="achievement-title">{{ achievement.title }}</h3>
            <p class="achievement-description">{{ achievement.description }}</p>
          </div>
        </div>
      </div>
    </section>
    
    <!-- 页脚信息 -->
    <footer class="profile-footer">
      <p>© {{ new Date().getFullYear() }} {{ personalInfo.name }} - 个人简介页</p>
      <p>by LSMX</p>
    </footer>
  </div>
</template>

<style scoped>
.profile-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 40px 20px;
  font-family: 'Helvetica Neue', Arial, sans-serif;
  color: #333;
  line-height: 1.6;
  background-color: #FFF0F5;
}

/* 照片部分样式 */
.photo-section {
  display: flex;
  justify-content: center;
  margin-bottom: 60px;
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.8s ease, transform 0.8s ease;
}

.photo-section.visible {
  opacity: 1;
  transform: translateY(0);
}

.photo-container {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  width: 600px;
  height: 300px;
  margin: 0 auto;
}

.photo-wrapper {
  position: relative;
  width: 300px;
  height: 300px;
  border-radius: 50%;
  overflow: hidden;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
  border: 8px solid white;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  z-index: 2;
}

.photo-wrapper:hover {
  transform: scale(1.05);
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.2);
}

.profile-photo {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.photo-wrapper:hover .profile-photo {
  transform: scale(1.08);
}

/* 社交图标样式 */
.social-icon {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 1;
}

.social-icon.left {
  left: 0;
}

.social-icon.right {
  right: 0;
}

.icon-wrapper {
  position: relative;
  width: 50px;
  height: 50px;
  background-color: white;
  border-radius: 50%;
  padding: 10px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
  cursor: pointer;
}

.icon-wrapper:hover {
  transform: scale(1.1);
}

.icon-image {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.qrcode-container {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background-color: white;
  padding: 10px;
  border-radius: 8px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.15);
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease;
  z-index: 10;
}

/* 电脑端二维码样式 */
@media (min-width: 769px) {
  .social-icon.left .qrcode-container {
    right: 100%;
    margin-right: 20px;
  }

  .social-icon.right .qrcode-container {
    left: 100%;
    margin-left: 20px;
  }

  .qrcode-container.show {
    opacity: 1;
    visibility: visible;
  }

  .qrcode-image {
    width: 120px;
    height: 120px;
    border-radius: 5px;
    display: block;
  }
}

/* 手机端二维码样式 */
@media (max-width: 768px) {
  .qrcode-container {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    margin: 0;
    z-index: 1000;
    background-color: white;
    padding: 15px;
    border-radius: 10px;
    box-shadow: 0 5px 30px rgba(0, 0, 0, 0.2);
  }

  .qrcode-image {
    width: 180px;
    height: 180px;
    border-radius: 5px;
    display: block;
  }

  /* 遮罩层 */
  .qrcode-container::before {
    content: '';
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: -1;
  }

  .qrcode-container.show {
    opacity: 1;
    visibility: visible;
  }
}

/* 个人简介部分样式 */
.info-section {
  text-align: center;
  margin-bottom: 70px;
  max-width: 800px;
  margin-left: auto;
  margin-right: auto;
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.8s ease, transform 0.8s ease;
}

.info-section.visible {
  opacity: 1;
  transform: translateY(0);
}

.name {
  font-size: 42px;
  font-weight: 700;
  margin: 0 0 8px 0;
  color: #2c3e50;
  text-shadow: 0 2px 2px rgba(0, 0, 0, 0.05);
}

.title {
  font-size: 24px;
  font-weight: 400;
  color: #3498db;
  margin: 0 0 20px 0;
}

.divider {
  width: 80px;
  height: 4px;
  background: linear-gradient(90deg, #3498db, #2980b9);
  margin: 0 auto 30px;
  border-radius: 2px;
}

.description {
  font-size: 18px;
  line-height: 1.8;
  color: #555;
  margin-bottom: 40px;
}

/* 技能展示部分 */
.skills-container {
  margin-top: 40px;
  background-color: white;
  padding: 40px;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  text-align: left;
}

.skills-title {
  text-align: center;
  font-size: 28px;
  margin-bottom: 35px;
  color: #2c3e50;
  font-weight: 600;
  position: relative;
  padding-bottom: 15px;
}

.skills-title::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 60px;
  height: 4px;
  background: linear-gradient(90deg, #3498db, #2980b9);
  border-radius: 2px;
}

.skill {
  margin-bottom: 25px;
  padding: 15px;
  background-color: #f8f9fa;
  border-radius: 10px;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.skill:hover {
  transform: translateX(5px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
}

.skill-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 12px;
  align-items: center;
}

.skill-name {
  font-weight: 600;
  color: #2c3e50;
  font-size: 18px;
}

.skill-level {
  color: #3498db;
  font-weight: 600;
  font-size: 18px;
  background-color: rgba(52, 152, 219, 0.1);
  padding: 4px 12px;
  border-radius: 15px;
}

.skill-bar {
  height: 12px;
  background-color: #e9ecef;
  border-radius: 6px;
  overflow: hidden;
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
}

.skill-progress {
  height: 100%;
  background: linear-gradient(90deg, #3498db, #2980b9);
  border-radius: 6px;
  width: 0;
  transition: width 1.5s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  overflow: hidden;
}

.skill-progress::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(
    90deg,
    rgba(255, 255, 255, 0) 0%,
    rgba(255, 255, 255, 0.2) 50%,
    rgba(255, 255, 255, 0) 100%
  );
  animation: shimmer 2s infinite;
}

@keyframes shimmer {
  0% {
    transform: translateX(-100%);
  }
  100% {
    transform: translateX(100%);
  }
}

.info-section.visible .skill-progress {
  animation: progressAnimation 2s cubic-bezier(0.4, 0, 0.2, 1) forwards;
}

@keyframes progressAnimation {
  from { width: 0; }
  to { width: attr(data-level); }
}

/* 个人事迹部分样式 */
.achievements-section {
  padding: 60px 0;
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.8s ease, transform 0.8s ease;
}

.achievements-section.visible {
  opacity: 1;
  transform: translateY(0);
}

.section-title {
  text-align: center;
  font-size: 32px;
  font-weight: 600;
  color: #2c3e50;
  margin-bottom: 50px;
  position: relative;
  text-shadow: 0 2px 2px rgba(0, 0, 0, 0.05);
}

.section-title::after {
  content: '';
  position: absolute;
  bottom: -15px;
  left: 50%;
  transform: translateX(-50%);
  width: 60px;
  height: 3px;
  background: linear-gradient(90deg, #3498db, #2980b9);
  border-radius: 2px;
}

/* 时间线样式 */
.timeline-container {
  position: relative;
  max-width: 1140px;
  margin: 0 auto;
}

.timeline-line {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 50%;
  width: 4px;
  background-color: #3498db;
  transform: translateX(-50%);
}

.achievement-card {
  position: relative;
  width: calc(50% - 40px);
  margin-bottom: 50px;
  background-color: white;
  border-radius: 10px;
  padding: 25px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.achievement-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
}

.achievement-card.right {
  margin-left: calc(50% + 40px);
}

.achievement-card.left {
  margin-right: calc(50% + 40px);
}

.achievement-dot {
  position: absolute;
  top: 20px;
  width: 20px;
  height: 20px;
  background-color: #3498db;
  border-radius: 50%;
  border: 4px solid white;
  box-shadow: 0 0 0 3px #3498db;
}

.achievement-card.right .achievement-dot {
  left: -50px;
}

.achievement-card.left .achievement-dot {
  right: -50px;
}

.achievement-year {
  display: inline-block;
  background-color: #3498db;
  color: white;
  font-weight: 600;
  font-size: 16px;
  padding: 5px 15px;
  border-radius: 20px;
  margin-bottom: 15px;
}

.achievement-title {
  font-size: 20px;
  font-weight: 600;
  margin-bottom: 10px;
  color: #2c3e50;
}

.achievement-description {
  font-size: 16px;
  color: #555;
  line-height: 1.7;
}

/* 页脚样式 */
.profile-footer {
  margin-top: 60px;
  text-align: center;
  font-size: 14px;
  color: #7f8c8d;
  padding: 20px 0;
  border-top: 1px solid #ecf0f1;
}

/* 响应式设计 */
@media (max-width: 768px) {
  .profile-container {
    padding: 20px 15px;
  }

  /* 照片部分适配 */
  .photo-container {
    flex-direction: row;
    width: 100%;
    height: auto;
    padding: 10px;
    justify-content: center;
    align-items: center;
    gap: 10px;
  }

  .photo-wrapper {
    width: 120px;
    height: 120px;
    margin: 0 5px;
  }

  .social-icon {
    position: relative;
    transform: none;
  }

  .social-icon.left,
  .social-icon.right {
    position: relative;
  }

  .icon-wrapper {
    width: 35px;
    height: 35px;
    padding: 6px;
  }

  /* 二维码弹窗优化 */
  .qrcode-container {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    margin: 0;
    z-index: 1000;
    background-color: white;
    padding: 15px;
    border-radius: 10px;
    box-shadow: 0 5px 30px rgba(0, 0, 0, 0.2);
  }

  .qrcode-image {
    width: 180px;
    height: 180px;
  }

  /* 遮罩层 */
  .qrcode-container::before {
    content: '';
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: -1;
  }

  /* 个人信息部分适配 */
  .info-section {
    padding: 0 15px;
    margin-bottom: 40px;
  }

  .name {
    font-size: 28px;
    margin-bottom: 5px;
  }
  
  .title {
    font-size: 18px;
    margin-bottom: 15px;
  }
  
  .description {
    font-size: 15px;
    line-height: 1.6;
    margin-bottom: 30px;
  }

  /* 技能展示部分适配 */
  .skills-container {
    padding: 20px;
    margin-top: 30px;
  }

  .skills-title {
    font-size: 24px;
    margin-bottom: 25px;
  }

  .skill {
    margin-bottom: 20px;
    padding: 12px;
  }

  .skill-name {
    font-size: 16px;
  }

  .skill-level {
    font-size: 14px;
    padding: 3px 10px;
  }

  .skill-bar {
    height: 10px;
  }

  /* 个人事迹部分适配 */
  .achievements-section {
    padding: 40px 0;
  }

  .section-title {
    font-size: 26px;
    margin-bottom: 30px;
  }

  .timeline-line {
    left: 20px;
  }
  
  .achievement-card {
    width: calc(100% - 40px);
    margin-left: 40px !important;
    margin-right: 0 !important;
    padding: 20px;
  }
  
  .achievement-card.right .achievement-dot,
  .achievement-card.left .achievement-dot {
    left: -30px;
    right: auto;
    width: 16px;
    height: 16px;
  }

  .achievement-year {
    font-size: 14px;
    padding: 4px 12px;
  }

  .achievement-title {
    font-size: 18px;
    margin-bottom: 8px;
  }

  .achievement-description {
    font-size: 14px;
    line-height: 1.6;
  }

  /* 页脚适配 */
  .profile-footer {
    margin-top: 40px;
    padding: 15px 0;
    font-size: 13px;
  }
}

/* 平板设备适配 */
@media (min-width: 768px) and (max-width: 1024px) {
  .profile-container {
    padding: 30px 20px;
  }

  .photo-wrapper {
    width: 200px;
    height: 200px;
  }

  .name {
    font-size: 36px;
  }

  .title {
    font-size: 22px;
  }

  .description {
    font-size: 17px;
  }

  .skills-container {
    padding: 30px;
  }

  .achievement-card {
    width: calc(50% - 30px);
  }
}
</style> 