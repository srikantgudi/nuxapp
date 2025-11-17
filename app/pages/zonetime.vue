
<script setup>
    import moment from 'moment-timezone';

    import ZonetimeSelector from '@/components/zoneselector.vue';
    import Clock from '@/components/clock.vue';

    let zone1 = ref('Asia/Kolkata');
    let zone2 = ref('Asia/Kolkata');
    let inputtime = ref(moment());

    const zone1time = computed(() => {
        if (inputtime.value) {
            return moment.tz(inputtime.value, zone1.value);
        } 
        return moment.tz(zone1.value);
    });
    const zone2time = computed(() => {
        return moment.tz(zone1time.value,zone2.value);
    });
</script>

<template>
    <h2>Zone times View</h2>
    <div class="vflex">
        <div class="dflex">
            <ZonetimeSelector selectlabel="Select Zone-1" v-model:zone="zone1" /> 
            <div>{{zone1}}</div>
            <div>{{zone1time.format("ddd DD-MMM HH:mm:ss a")}}</div>
            <label for="inputtime">
                Select custom time:
                <input type="datetime-local" v-model="inputtime" id="inputtime">
            </label>
        </div>
        <div class="dflex">
            <ZonetimeSelector selectlabel="Select Zone-2" v-model:zone="zone2" />
            <div>{{zone2}}</div>
            <div>{{zone2time.format("ddd DD-MMM HH:mm:ss a")}}</div>
        </div>
    </div>
    <div class="dflex">
        <Clock :zone="zone1" :ztime="zone1time" />
        <Clock :zone="zone2" :ztime="zone2time" />
    </div>
</template>
