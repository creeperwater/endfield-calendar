<template>
  <div class="project">
    <div class="key">
      <div class="key-stripe-bg"></div>
      <div class="key-main">
        <!-- Abstract watermark logo -->
        <div class="key-bg-logo">
          <div class="logo-inner"></div>
        </div>
        <!-- Decorative subtle pattern -->
        <div class="key-bg-pattern"></div>
        
        <!-- Text content -->
        <div class="key-title-wrap">
          <div class="key-subtitle-box">注</div>
          <div class="key-title">{{ category }}</div>
        </div>
        
        <!-- UI Accents -->
        <div class="key-vertical-line"></div>
        <div class="key-nav-dots">
          <div class="dot"></div>
          <div class="dot"></div>
          <div class="dot active"></div>
        </div>
      </div>
    </div>
    <div class="value">
      <div class="project-grid" :style="{ gridTemplateColumns: gridColumns }">
        <Item
          v-for="task in categoryTasks"
          :key="task.id"
          :task="task"
          :start="start"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Item from './Item.vue'

export default {
  name: 'Project',
  components: { Item },
  props: {
    category: { type: String, required: true },
    tasks: { type: Array, required: true },
    gridColumns: { type: String, required: true },
    start: { type: String, required: true }
  },
  computed: {
    categoryTasks() {
      return this.tasks.filter(t => (t.category || '未分类') === this.category)
    }
  }
}
</script>

<style scoped>
.project {
  display: flex;
  border-bottom: 2px solid #ebebeb;
  min-height: 120px;
}

.key {
  width: 200px;
  flex-shrink: 0;
  display: flex;
  background: white;
  border-left: 2px solid #1a1a1a;
  position: relative;
  overflow: hidden;
  box-sizing: border-box;
}

.key-stripe-bg {
  width: 35%;
  background: repeating-linear-gradient(
    -45deg,
    #ededed,
    #ededed 4px,
    #f8f8f8 4px,
    #f8f8f8 8px
  );
  border-right: 2px solid #e1f46d;
  z-index: 1;
}

.key-main {
  width: 65%;
  background: #c3d687;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  overflow: hidden;
}

.key-bg-logo {
  position: absolute;
  top: -15px;
  right: -25px;
  width: 100px;
  height: 100px;
  border: 14px solid rgba(255, 255, 255, 0.8);
  border-radius: 50%;
  border-top-color: transparent;
  transform: rotate(-30deg);
  pointer-events: none;
}

.key-bg-logo .logo-inner {
  position: absolute;
  top: 15px;
  left: 20px;
  width: 25px;
  height: 45px;
  background: rgba(255, 255, 255, 0.8);
  transform: rotate(45deg);
}

.key-bg-pattern {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 60px;
  height: 60px;
  background: rgba(255, 255, 255, 0.15);
  border-top-right-radius: 100%;
  pointer-events: none;
}

.key-title-wrap {
  z-index: 2;
  display: flex;
  align-items: center;
  margin-right: 20px;
  transform: translateY(-10px);
}

.key-subtitle-box {
  width: 12px;
  height: 12px;
  border: 1px solid #d24e39;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #d24e39;
  font-size: 10px;
  margin-right: 4px;
  font-family: sans-serif;
  transform: scale(0.8);
}

.key-title {
  font-family: "Noto Serif SC", "SimSun", serif;
  font-size: 24px;
  color: #2c3320;
  letter-spacing: 2px;
}

.key-vertical-line {
  position: absolute;
  right: 20px;
  top: 50%;
  height: 35%;
  width: 1px;
  background: #5b6540;
}

.key-vertical-line::before,
.key-vertical-line::after {
  content: "";
  position: absolute;
  left: -2px;
  width: 3px;
  height: 3px;
  border: 1px solid #5b6540;
  border-radius: 50%;
  background: #c3d687;
}

.key-vertical-line::before { top: 0; }
.key-vertical-line::after { bottom: 0; }

.key-nav-dots {
  position: absolute;
  bottom: 8px;
  right: 17px;
  display: flex;
  gap: 4px;
  align-items: center;
}

.key-nav-dots .dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  border: 1px solid rgba(255, 255, 255, 0.8);
  box-sizing: border-box;
}

.key-nav-dots .dot.active {
  border-color: #d24e39;
}

.value {
  flex: 1;
  overflow-x: auto; 
  background: #fff;
}

.project-grid {
  display: grid;
  min-height: 100%; 
  grid-auto-rows: 40px; 
  grid-auto-flow: row dense;
  gap: 4px 0;
  padding: 8px 0;
  box-sizing: border-box;
}

.value::-webkit-scrollbar {
  height: 8px;
}
.value::-webkit-scrollbar-thumb {
  background: #ddd;
  border-radius: 4px;
}
</style>
