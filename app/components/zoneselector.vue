<template>
  <div>
    {{selectlabel}}: 
    <select id="zone" v-model="selectedZone" @change="hey ">
      <!-- <option value="">Local</option> -->
      <option v-for="z in zones" :key="z" :value="z">{{ z }}</option>
    </select>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

// The zone prop is passed from the parent to initialize selectedZone
const props = defineProps({
  selectlabel: {
    type: String,
    required: true,
  },
  zone: {
    type: String,
    required: true,
  },
});

// The emit function to update parent on changes
const emit = defineEmits(['update:zone']); 

// List of available zones
const zones = [
  'America/Los_Angeles',
  'America/New_York',
  'Europe/London',
  'Europe/Paris',
  'Europe/Moscow',
  'Asia/Kathmandu',
  'Asia/Kolkata',
  'Asia/Tokyo',
  'Australia/Sydney',
  'Pacific/Auckland'
];

// Local selected zone, default to the prop value (or empty string if not provided)
const selectedZone = ref(props.zone || '');

// Watch for changes in selectedZone and emit to the parent
watch(selectedZone, (newZone) => {
  emit('update:zone', newZone);
});
</script>