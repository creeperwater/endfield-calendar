<template>
  <div class="app">
    <Title />
    <Timeline 
      :days="days" 
      :gridColumns="gridColumns"
      :scheduleStart="scheduleStart"
      :scheduleEnd="scheduleEnd"
    />
    <div class="content">
      <Project
        v-for="cat in categories"
        :key="cat"
        :category="cat"
        :tasks="tasks"
        :gridColumns="gridColumns"
        :start="start"
      />
    </div>
    <Footer />
  </div>
</template>

<script>
import Title from './components/Title.vue'
import Timeline from './components/Timeline.vue'
import Project from './components/Project.vue'
import Footer from './components/Footer.vue'

export default {
  components: { Title, Timeline, Project, Footer },
  data() {
    const tasks = [
      { id: 1, name: '需求分析', category: '研发', start: '2026-04-01', end: '2026-04-05' },
      { id: 7, name: '架构演进', category: '研发', start: '2026-04-02', end: '2026-04-10' },
      { id: 2, name: 'UI 设计', category: '设计', start: '2026-04-03', end: '2026-04-10' },
      { id: 3, name: '前端实现', category: '研发', start: '2026-04-06', end: '2026-04-18' },
      { id: 6, name: '后端研发', category: '研发', start: '2026-04-04', end: '2026-04-14' },
      { id: 4, name: '测试', category: 'QA', start: '2026-04-15', end: '2026-04-22' },
      { id: 5, name: '部署', category: '运维', start: '2026-04-23', end: '2026-04-24' }
    ]

    // auto compute overall start/end with padding
    const minDate = tasks.reduce((m, t) => (new Date(t.start) < m ? new Date(t.start) : m), new Date(tasks[0].start))
    const maxDate = tasks.reduce((m, t) => (new Date(t.end) > m ? new Date(t.end) : m), new Date(tasks[0].end))

    const start = new Date(minDate)
    start.setDate(start.getDate() - 2)
    const end = new Date(maxDate)
    end.setDate(end.getDate() + 2)

    return { 
      tasks, 
      start: start.toISOString().slice(0,10), 
      end: end.toISOString().slice(0,10), 
      scheduleStart: new Date(minDate).toISOString().slice(0,10),
      scheduleEnd: new Date(maxDate).toISOString().slice(0,10),
      pxPerDay: 40 
    }
  },
  computed: {
    days() {
      const s = new Date(this.start)
      const e = new Date(this.end)
      const daysArr = []
      let cur = new Date(s)
      while (cur <= e) {
        daysArr.push({ date: cur.toISOString().slice(0,10), label: `${cur.getMonth()+1}/${cur.getDate()}` })
        cur = new Date(cur)
        cur.setDate(cur.getDate() + 1)
      }
      return daysArr
    },
    categories() {
      return [...new Set(this.tasks.map(t => t.category || '未分类'))]
    },
    gridColumns() {
      return `repeat(${this.days.length}, ${this.pxPerDay}px)`
    }
  }
}
</script>

<style scoped>
.app {
  display: flex;
  flex-direction: column;
  height: 100vh;
  box-sizing: border-box;
}

.content {
  display: flex;
  flex-direction: column;
  flex: 1;
  overflow-y: auto;
  overflow-x: hidden;
  background: white;
}
</style>
