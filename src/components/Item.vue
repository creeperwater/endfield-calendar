<template>
  <div
    class="task-cell"
    :style="taskStyle"
    :title="task.name + ' (' + task.start + ' → ' + task.end + ')'"
  >
    <div class="task-inner">{{ task.name }}</div>
  </div>
</template>

<script>
export default {
  name: 'Item',
  props: {
    task: { type: Object, required: true },
    start: { type: String, required: true }
  },
  computed: {
    taskStyle() {
      const s = new Date(this.start)
      const d1 = new Date(this.task.start)
      const d2 = new Date(this.task.end)
      
      const startIdx = Math.round((d1 - s) / (1000 * 60 * 60 * 24))
      const endIdx = Math.round((d2 - s) / (1000 * 60 * 60 * 24))
      const span = Math.max(endIdx - startIdx + 1, 1)
      
      return {
        gridColumn: `${startIdx + 1} / span ${span}`
      }
    }
  }
}
</script>

<style scoped>
.task-cell {
  position: relative;
  padding: 2px 4px;
  box-sizing: border-box;
}

.task-inner {
  background: linear-gradient(90deg, #1b2b3a 0%, #3a4b5c 100%);
  color: #fff;
  padding: 4px 12px;
  border-radius: 2px;
  border-left: 4px solid #ccff00;
  height: 100%;
  width: 100%;
  display: flex;
  align-items: center;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  box-sizing: border-box;
  box-shadow: 2px 2px 6px rgba(0,0,0,0.15);
}
</style>
