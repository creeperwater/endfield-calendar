<template>
  <div class="timeline" ref="timeline">
    <div class="timeline-empty-key">
    </div>
    <div class="timeline-grid-wrapper">
      <div class="timeline-grid" :style="{ gridTemplateColumns: gridColumns }">
        <template v-for="(d, index) in days" :key="d.date">
          <!-- Month tag -->
          <div 
            v-if="d.date.endsWith('-01') || index === 0" 
            class="month-label"
            :style="{ gridColumn: index + 1 }"
          >
            {{ parseInt(d.date.split('-')[1]) }}月
          </div>
          <!-- Day number -->
          <div class="day-cell" :style="{ gridColumn: index + 1, gridRow: 2 }">
            {{ d.date.split('-')[2] }}
          </div>
        </template>
        
        <!-- Start Marker -->
        <div v-if="startMarkerIndex > 0" class="date-marker start-marker" :style="{ gridColumn: startMarkerIndex }">
          <div class="marker-border"></div>
          <div class="marker-text">
            {{ formatMarker(scheduleStart) }}
          </div>
        </div>
        
        <!-- End Marker -->
        <div v-if="endMarkerIndex > 0" class="date-marker end-marker" :style="{ gridColumn: endMarkerIndex }">
          <div class="marker-border"></div>
          <div class="marker-text">
            {{ formatMarker(scheduleEnd) }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Timeline',
  props: {
    days: { type: Array, required: true },
    gridColumns: { type: String, required: true },
    scheduleStart: { type: String, required: false },
    scheduleEnd: { type: String, required: false }
  },
  computed: {
    startMarkerIndex() {
      if (!this.scheduleStart) return -1;
      const idx = this.days.findIndex(d => d.date === this.scheduleStart);
      return idx >= 0 ? idx + 1 : -1;
    },
    endMarkerIndex() {
      if (!this.scheduleEnd) return -1;
      const idx = this.days.findIndex(d => d.date === this.scheduleEnd);
      return idx >= 0 ? idx + 1 : -1;
    }
  },
  methods: {
    formatMarker(dateStr) {
      if (!dateStr) return '';
      const parts = dateStr.split('-');
      if (parts.length === 3) {
        return `${parts[1]}.${parts[2]}`;
      }
      return dateStr;
    }
  }
}
</script>

<style scoped>
.timeline {
  display: flex;
  flex-shrink: 0;
  border-bottom: 2px solid #ddd;
  overflow: hidden;
  background: #ebebeb;
  height: 60px;
}

.timeline-empty-key {
  width: 200px;
  flex-shrink: 0;
  background: #f5f5f5;
  border-right: 1px solid #dcdcdc;
  position: relative;
  display: flex;
  align-items: flex-end;
  padding-bottom: 8px;
  padding-left: 12px;
}

.timeline-grid-wrapper {
  flex: 1;
  overflow: hidden;
  position: relative;
}

.timeline-grid {
  display: grid;
  height: 100%;
  grid-template-rows: 1fr 1fr;
}

.month-label {
  grid-row: 1;
  font-size: 12px;
  font-weight: bold;
  color: #fff;
  background: #d4d4d4;
  align-self: end;
  justify-self: start;
  padding: 0 4px;
  border-radius: 2px;
  margin-left: 4px;
  transform: translateY(4px);
  z-index: 1;
}

.day-cell {
  color: #fff;
  font-weight: bold;
  font-size: 14px;
  display: flex;
  align-items: flex-end;
  justify-content: center;
  padding-bottom: 4px;
  position: relative;
}

/* Light separation lines between days */
.day-cell::after {
  content: "";
  position: absolute;
  right: 0;
  bottom: 4px;
  width: 1px;
  height: 4px;
  background: #dcdcdc;
}

/* Markers */
.date-marker {
  grid-row: 1 / 3;
  position: relative;
  display: flex;
  align-items: center;
  z-index: 10;
  width: 80px; 
}

.start-marker {
  justify-content: flex-start;
  transform: translateX(-10px);
}

.end-marker {
  justify-content: flex-start;
  transform: translateX(-10px);
}

.marker-border {
  position: absolute;
  left: 0;
  top: 10px;
  bottom: 0px;
  width: 2px;
  background-color: #9cb121; /* Green color from image */
}

/* Dots along the border */
.marker-border::before, .marker-border::after {
  content: "";
  position: absolute;
  left: -2px;
  width: 6px;
  height: 2px;
  background-color: #9cb121;
}
.marker-border::before { top: 0; }
.marker-border::after { bottom: 0; }

.marker-text {
  background-color: #a5c328;
  color: #fff;
  font-weight: 900;
  font-size: 20px;
  line-height: 1;
  padding: 4px 8px;
  margin-left: 2px;
  border: 1px solid #7a8e1b;
  position: relative;
  letter-spacing: 1px;
}

.marker-text::after {
  content: "";
  position: absolute;
  top: 2px;
  left: 2px;
  width: 6px;
  height: 6px;
  border-top: 2px solid #fff;
  border-left: 2px solid #fff;
}
</style>
