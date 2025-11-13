<template>
    <div class="vflex">
        <h2>Clock for :: {{zone}}</h2>
        <div>
          <svg viewBox="-50 -50 100 100" width="400">
              <circle r="49" fill="lightcyan" stroke="navy" stroke-width="0.5" />
              <line class="hand" x1="-4" x2="32" :stroke="handclr" stroke-linecap="round" :transform="`rotate(${ang.h})`" />
              <line class="hand" x1="-4" x2="42" :stroke="handclr" stroke-linecap="round" :transform="`rotate(${ang.m})`" />
          </svg>
        </div>
    </div>
</template>

<script setup>
import { DateTime } from 'luxon';
import { computed } from 'vue';

// Define props with a default value (current time)
const props = defineProps({
    zone: {
        type: String,
        required: true
    },
    ztime: {
        type: DateTime,
        default: DateTime.now() // Default value is the current time
    }
});

// Create a computed property to calculate the angles
const handclr = computed(() => {
  let clr = '#333';
  const hr = props.ztime.hour;
  if (hr < 3) clr = '#333';
  else if (hr < 6) clr = '#666';
  else if (hr < 12) clr = 'blue';
  else if (hr < 18) clr = 'seagreen';
  else clr = 'navy';
});

const ang = computed(() => {
  const ztime = props.ztime; // Get the ztime prop from the parent
  return {
    h: (ztime.hour * 30 + ztime.minute / 2) - 90,  // Hour hand angle (12-hour clock)
    m: (ztime.minute * 6 + ztime.second / 10) - 90, // Minute hand angle
  };
});
</script>
