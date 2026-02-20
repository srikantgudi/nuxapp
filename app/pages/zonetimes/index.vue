<template>
    <div>
        <div class="text-3xl">Zone times</div>

        <div class="grid grid-cols-4 gap-1">
            <div>
                <div class="my-2 text-2xl">Regions</div>
                <div class="my-2 text-xl text-amber-600">&raquo; {{region}}</div>
                <select class="shadow-md shadow-gray-600 rounded-sm" v-model="region" :size="regions.length" id="">
                    <option class="p-1" v-for="r in regions">
                        {{r}}
                    </option>
                </select>
                
            </div>
            <div>
                <div class="my-2 text-2xl">Zones</div>
                <div class="my-2 text-xl text-blue-600">&raquo; {{zone}}</div>
                <div>
                    <select class="shadow-md shadow-gray-600 rounded-ms" v-model="zone" size="20">
                        <option class="p-1" v-for="rz in regionzones">{{rz}}</option>
                    </select>
                    
                </div>
            </div>
            <div>
                <div class="mb-4 text-2xl">Clock</div>
                <div v-if="zone" class="text-[navy] font-bold"><i>Zone time: </i>{{zonetimeFmt}}</div>
                <div v-else>- Select zone -</div>
                <div class="flex flex-col gap-1 m-auto">
                    <div>
                        <svg viewBox="-50 -50 100 100" width="300">
                            <circle r="49" fill="lightcyan" stroke="darkslateblue" stroke-width="0.5" />
                            <polyline points="-4,0 4,-1 30,0 4,1 -4,0" :transform="`rotate(${hrangle})`"  />
                            <polyline points="-4,0 4,-1 42,0 4,1 -4,0" :transform="`rotate(${miangle})`"  />
                        </svg>
                    </div>
                    <div class="p-2 bg-amber-100 w-9/10 flex flex-col items-center m-auto">
                        <div class="text-[maroon] font-bold"><i>Local time: </i>{{inputdtCompFmt.toLocaleString()}}</div>
                        <svg viewBox="-50 -50 100 100" width="200">
                            <circle r="49" fill="#fd9" stroke="maroon" stroke-width="0.5" />
                            <line x1="-8" x2="30" stroke-linecap="round" stroke="maroon" :transform="`rotate(${hrangleloc})`"  />
                            <line x1="-8" x2="42" stroke-linecap="round" stroke="maroon" :transform="`rotate(${miangleloc})`"  />
                        </svg>
                    </div>
                </div>
            </div>
            <div>
                <div class="text-2xl">Custom time</div>
                <div>
                    Select date: <input type="datetime-local" v-model="inputdt" class="p-1 shadow-md shadow-gray-400" />
                    <button @click="console.log('BEFORE:', inputdt.value); inputdt=''; console.log('AFTER:', inputdt.value);"" class="bg-gray-300 rounded-sm p-1">&times; Clear</button>
                    <div>{{inputdt.toLocaleString()}}</div>
                </div>
                <div class="my-4 p-4 bg-gray-200">
                    Select a time as local time, and then another zone, to view corresponding time in the zone..
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
    import {ref, reactive, computed, onMounted} from 'vue';

    const weekdays = ['Sun','Mon','Tue','Wed','Thu','Fri','Sat'];
    let region = ref('Asia');
    let zone = ref('Asia/Calcutta');
    const zones = ref( Intl.supportedValuesOf('timeZone'));
    const regions = computed(() => Array.from(new Set(zones.value.map(z => z.slice(0,z.indexOf('/'))))));
    const regionzones = computed(() => {
        const rzones = zones.value.filter(z => z.includes(region.value));
        return rzones;
        }
    )
    let basedate = computed(() => new Date());
    let inputdt = ref('');
    const inputdtComp = computed(() => inputdt.value ? new Date(inputdt.value) : new Date());
    const zonetime = computed(() => zone.value ? new Date(new Date(inputdtComp.value).toLocaleString('en-US',{timeZone: zone.value})) : new Date());
    const hrangle = computed(() => zone.value ? (zonetime.value.getHours() * 30 + zonetime.value.getMinutes()/2) - 90 : 0);
    const miangle = computed(() => zone.value ? (zonetime.value.getMinutes() * 6 + zonetime.value.getSeconds()/10) - 90 : 0);
    const hrangleloc = computed(() => zone.value ? (inputdtComp.value.getHours() * 30 + inputdtComp.value.getMinutes()/2) - 90 : 0);
    const miangleloc = computed(() => zone.value ? (inputdtComp.value.getMinutes() * 6 + inputdtComp.value.getSeconds()/10) - 90 : 0);

    const zonetimeFmt = computed(() => new Intl.DateTimeFormat('en-US',{weekday:'short',hour:'numeric',minute:'numeric',day:'numeric',month:'short',timeZoneName:'short',timeZone:zone.value}).format(zonetime.value))
    const inputdtCompFmt = computed(() => new Intl.DateTimeFormat('en-US',{weekday:'short',hour:'numeric',minute:'numeric',day:'numeric',month:'short',timeZoneName:'short',timeZone:zone.value}).format(inputdtComp.value))
    
</script>