<template>
  <div class="title-container">
    <!-- 背景大字水印 -->
    <div class="bg-watermark">SCHEDULE</div>
    
    <!-- 左侧标题区域 -->
    <div class="title-left">
      <div class="dec-lines">
        <span class="dot"></span>
        <span class="dot-empty"></span>
      </div>
      <div class="main-text">
        <!-- 模仿框选的重磅字体 -->
        <div class="box-text">大三下</div>
        <div class="plain-text">日程</div>
      </div>
      <div class="sub-text">
        <span class="tri">▼</span> THE JUNIOR YEAR SPRING SEMESTER <span class="tri">▼</span>
      </div>
    </div>

    <!-- 右侧 Logo/隶属 区域 -->
    <div class="title-right">
      <div class="logo-top">HEFEI UNIVERSITY OF TECHNOLOGY</div>
      <div class="logo-main">
        合肥工业大学
      </div>
      <div class="logo-bottom">
        HFUT SCHEDULE <span class="red-blocks">■ ■ ■</span>
      </div>
    </div>
    
    <!-- 底部特有装饰线 (红线与黑线) -->
    <div class="bottom-bar">
      <div class="bar-red"></div>
      <div class="bar-black"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Title'
}
</script>

<style scoped>
.title-container {
  position: relative;
  height: 120px;
  background: linear-gradient(105deg, #f8fbf4 0%, #e2f7c0 50%, #c8ea94 100%);
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 60px;
  overflow: hidden;
  flex-shrink: 0;
  border-bottom: 4px solid transparent; /* reserved for bottom-bar */
}

/* 淡淡网格背景 */
.title-container::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0; bottom: 0;
  background-image: 
    linear-gradient(rgba(0,0,0,0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0,0,0,0.03) 1px, transparent 1px);
  background-size: 20px 20px;
  z-index: 0;
}

.bg-watermark {
  position: absolute;
  top: -15px;
  left: 25%;
  font-size: 130px;
  color: rgba(255, 255, 255, 0.45);
  font-family: 'Arial Black', Impact, sans-serif;
  letter-spacing: 20px;
  pointer-events: none;
  user-select: none;
  z-index: 0;
}

.title-left {
  position: relative;
  z-index: 1;
  display: flex;
  flex-direction: column;
}

.dec-lines {
  margin-bottom: 8px;
  display: flex;
  gap: 4px;
}
.dot {
  display: inline-block;
  width: 4px; height: 4px;
  background: #d32f2f;
  border-radius: 50%;
}
.dot-empty {
  display: inline-block;
  width: 4px; height: 4px;
  border: 1px solid #d32f2f;
  border-radius: 50%;
  box-sizing: border-box;
}

.main-text {
  display: flex;
  align-items: flex-end;
  gap: 8px;
}

.box-text {
  font-family: 'Noto Serif SC', 'SimSun', serif;
  font-size: 42px;
  font-weight: 900;
  color: #111;
  border: 2px solid #111;
  padding: 0px 10px;
  background: rgba(255, 255, 255, 0.7);
  box-shadow: 3px 3px 0 rgba(0,0,0,0.05);
  letter-spacing: 2px;
  line-height: 1.2;
}

.plain-text {
  font-family: 'Noto Serif SC', 'SimSun', serif;
  font-size: 40px;
  font-weight: 900;
  color: #111;
  letter-spacing: 4px;
  line-height: 1.2;
}

.sub-text {
  font-size: 11px;
  font-family: Arial, Helvetica, sans-serif;
  color: #222;
  margin-top: 8px;
  letter-spacing: 2px;
  font-weight: bold;
  padding-left: 10px;
}

.tri {
  font-size: 8px;
  color: #111;
}

.title-right {
  position: relative;
  z-index: 1;
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  text-align: right;
  padding-right: 20px;
}

.logo-top {
  font-size: 10px;
  font-family: sans-serif;
  font-weight: bold;
  color: rgba(255, 255, 255, 0.9);
  letter-spacing: 2px;
}

.logo-main {
  font-family: 'Noto Serif SC', 'SimSun', serif;
  font-size: 38px;
  font-weight: 900;
  line-height: 1.05;
  color: #fff;
  text-shadow: 0px 2px 6px rgba(120, 180, 80, 0.6);
  margin: 6px 0;
  letter-spacing: 2px;
}

.logo-bottom {
  font-size: 10px;
  font-family: sans-serif;
  font-weight: bold;
  color: rgba(255, 255, 255, 0.95);
  letter-spacing: 1px;
}
.red-blocks {
  color: #d32f2f;
  margin-left: 6px;
  font-size: 10px;
  letter-spacing: 2px;
}

.bottom-bar {
  position: absolute;
  bottom: 0; left: 0; right: 0;
  display: flex;
  flex-direction: column;
}

.bar-red {
  height: 3px;
  background: #d32f2f;
  width: 100%;
}

.bar-black {
  height: 2px;
  background: #2a2a2a;
  width: 100%;
  margin-top: 2px;
}
</style>
