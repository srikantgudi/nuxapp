<template>
    <h2>Zone times View</h2>
    <div class="vflex">
        <div class="dflex">
            <ZonetimeSelector selectlabel="Select Zone-1" v-model:zone="zone1" /> 
            <div>{{zone1}}</div>
            <div>{{zone1time.toFormat("EEE dd-MMM HH:mm:ss a")}}</div>
            <label for="inputtime">
                Select custom time:
                <input type="datetime-local" v-model="inputtime" id="inputtime">
            </label>
        </div>
        <div class="dflex">
            <ZonetimeSelector selectlabel="Select Zone-2" v-model:zone="zone2" />
            <div>{{zone2}}</div>
            <div>{{zone2time.toFormat("EEE dd-MMM HH:mm:ss a")}}</div>
        </div>
    </div>
    <div class="dflex">
        <Clock :zone="zone1" :ztime="zone1time" />
        <Clock :zone="zone2" :ztime="zone2time" />
    </div>
</template>

<script setup>
    import { DateTime } from 'luxon';
    import ZonetimeSelector from '@/components/zoneselector.vue';
    import Clock from '@/components/clock.vue';

    let zone1 = ref('Asia/Kolkata');
    let zone2 = ref('Asia/Kolkata');
    let inputtime = ref(DateTime.now());

    const zone1time = computed(() => {
        if (inputtime.value) {
            const parsedTime = DateTime.fromISO(inputtime.value);
            if (parsedTime.isValid) {
                return parsedTime.setZone(zone1.value);
            } else {
                console.error("Invalid time format");
                return DateTime.now().setZone(zone1.value); // Fallback to current time if invalid
            }
        }
        return DateTime.now().setZone(zone1.value);
    });
    const zone2time = computed(() => {
        return inputtime.value ? zone1time.value.setZone(zone2.value) : DateTime.now().setZone(zone2.value);
    });

</script>