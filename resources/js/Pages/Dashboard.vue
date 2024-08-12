<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import Checkbox from '@/Components/Checkbox.vue';
import { Head } from '@inertiajs/vue3';
import { ref } from 'vue'

const selected = ref('');
const selectedRm = ref('');
const proxyChecked = ref('');
const kapasitas = ref('');

// const form = useForm({
//     snack_pagi: false,
//     makan_siang: false,
//     snack_sore: false
// });
</script>

<template>
    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">Dashboard</h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <form>
                        <div class="p-6 text-gray-900">
                            <span class="text-black-600"><b>Informasi Ruang Meeting</b></span>
                        </div>
                        <div class="p-6 text-gray-900">
                            <div class="flex flex-col gap-3">
                                <div class="flex flex-row gap-2">
                                    <div class="mt-1">
                                        <label for="unit" class="block text-sm font-medium text-gray-700">
                                            <b>Unit</b>
                                        </label>
                                        <select id="unit" v-model="selected" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50">
                                            <option disabled value="" selected>Pilih Unit</option>
                                            <option v-for="unit in units" :value="unit.officeName">
                                                {{ unit.officeName }}
                                            </option>
                                        </select>
                                        <!-- <h1>Value:
                                            {{selected.id}}
                                        </h1> -->
                                    </div>
                                    <div class="mt-1">
                                        <label for="meeting_room" class="block text-sm font-medium text-gray-700">
                                            <b>Ruang Meeting</b>
                                        </label>
                                        <select id="meeting_room"  v-model="selectedRm" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50">
                                            <option disabled value="" selectedRm>Pilih Ruang Meeting</option>
                                            <option v-for="meeting_room in meeting_rooms" :value="meeting_room.id">
                                                {{ meeting_room.roomName }}
                                            </option>
                                        </select>
                                    </div>
                                </div>
                            </div>
                            <div class="flex flex-col gap-3">
                                <div class="flex flex-row gap-2">
                                    <div class="mt-2">
                                        <div class="mt-2">
                                            <label class="text-sm">
                                                <b>Kapasitas</b>
                                            </label>
                                            <input type="text" class="rounded border-gray-300 w-full">
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="p-6 text-gray-900">
                            <span class="text-black-600"><b>Informasi Rapat</b></span>
                            <div class="flex flex-col gap-3">
                                <div class="flex flex-row gap-2">
                                    <div class="mt-2">
                                        <label class="text-sm">
                                            <b>Tanggal Rapat</b>
                                        </label>
                                        <input type="date" class="rounded border-gray-300 w-full">
                                    </div>
                                    <div class="mt-2">
                                        <label class="text-sm">
                                            <b>Waktu Mulai</b>
                                        </label>
                                        <input type="time" class="rounded border-gray-300 w-full">
                                    </div>
                                    <div class="mt-2">
                                        <label class="text-sm">
                                            <b>Waktu Selesai</b>
                                        </label>
                                        <input type="time" class="rounded border-gray-300 w-full">
                                    </div>
                                </div>
                            </div>
                            <div class="flex flex-col gap-3">
                                <div class="flex flex-row gap-2">
                                    <div class="mt-2">
                                        <div class="mt-2">
                                            <label class="text-sm">
                                                <b>Jumlah Peserta</b>
                                            </label>
                                            <input type="text" class="rounded border-gray-300 w-full">
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="p-6 text-gray-900">
                            <span class="text-black-600"><b>Konsumsi Rapat</b></span>
                            <div class="block mt-2">
                                <label v-for="konsum in konsumsi" class="flex items-center">
                                    <input
                                        type="checkbox"
                                        v-bind:value="{ id: konsum.name, maxPrice: konsum.maxPrice }"
                                        v-model="proxyChecked"
                                        class="rounded border-gray-300 text-indigo-600 shadow-sm focus:ring-indigo-500"
                                    />
                                    <span class="ms-2 text-sm text-gray-600"><b>{{ konsum.name }}</b></span>
                                </label>
                                <!-- {{ konsum.id }} -->
                            </div>
                        </div>
                        <div class="p-6 text-gray-900">
                            <span class="text-black-600"><b>Nominal Konsumsi</b></span>
                            <div class="flex flex-col gap-3">
                                <div class="flex flex-row gap-2">
                                    <div class="mt-2">
                                        <input type="text" class="rounded border-gray-300 w-full">
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="p-6 text-gray-900">
                            <button @click="add" type="button" class="text-red-600 px-3 py-2 mt-4 font-semibold">
                                Batal
                            </button>
    
                            <button @click="update" type="button" class="bg-blue-600 text-white px-3 py-2 rounded mt-4 font-semibold ml-2">
                                Simpan
                            </button>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
<script>
export default {
    computed: {
      getAutofill(){
        // console.log(this.meeting_rooms);
        if (!this.meeting_rooms.find(item => item.id == this.selectedRm)) return ["",""]
        return this.meeting_rooms.find(item => item.id == this.selectedRm)
      }
    },
    data() {
        return {
            selected: '',
            proxyChecked: '',
            selectedRm: '',
            // kapasitas: undefined,
            units: [],
            meeting_rooms: [],
            konsumsi: []   
        };
    },
    mounted() {
        this.fetchData();
        this.fetchMeetingRoom();
        this.fetchKonsumsi(); 
    },
    methods: {
        fetchData() {
            axios.get('https://6666c7aea2f8516ff7a4e261.mockapi.io/api/dummy-data/masterOffice')
                .then(response => {
                    const data  = JSON.parse(JSON.stringify(response.data));
                    this.units  = data;
                })
                .catch(error => {
                    console.error('Error fetching data:', error);
                });   
        },
        fetchMeetingRoom() {
            axios.get('https://6666c7aea2f8516ff7a4e261.mockapi.io/api/dummy-data/masterMeetingRooms')
                .then(response => {
                    const data = JSON.parse(JSON.stringify(response.data));
                    this.meeting_rooms = data;
                //    console.log(Event.target.value);
                })
                .catch(error => {
                    console.error('Error fetching data:', error);
                });
        },
        fetchKonsumsi() {
            axios.get('https://6686cb5583c983911b03a7f3.mockapi.io/api/dummy-data/masterJenisKonsumsi')
                .then(response => {
                    const data = JSON.parse(JSON.stringify(response.data));
                    this.konsumsi = data;
                    //console.log(this.konsumsi);
                })
                .catch(error => {
                    console.error('Error fetching data:', error);
                });
        },
    },
};
</script>

