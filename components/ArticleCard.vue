<script setup>
import { initFlowbite } from 'flowbite'
import { defineProps, ref, onMounted, computed } from 'vue'

onMounted(() => {
    initFlowbite();
})

const props = defineProps({
    items: Object
})

const page = ref(1);
const perPage = ref(4);
const paginatedItems = computed(() => {
    const start = (page.value - 1) * perPage.value;
    const end = start + perPage.value;
    return props.items.slice(start, end);
});

const paper = ref({});
const paperDialog = ref(false);
const seePaperDetails = (item) => {
    paper.value = { ...item };
    paperDialog.value = true;
};
</script>

<template>
    <div class="grid gap-8 lg:grid-cols-2">
        <article
            class="p-6 bg-white rounded-lg plus-jakarta-sans-regular border border-gray-200 shadow-md dark:bg-gray-800 dark:hover:shadow-blue-900 hover:shadow-blue-100 dark:border-gray-700 hover:scale-105 transition duration-500 hover:cursor-pointer hover:shadow-xl hover:border-gray-300 dark:hover:border-gray-600"
            v-for="item in paginatedItems">
            <div class="flex justify-between items-center mb-5 text-gray-500">
                <span
                    class="bg-blue-100 text-blue-500 text-xs font-medium inline-flex items-center px-2.5 py-0.5 rounded dark:bg-blue-600 dark:text-white max-w-[50%] overflow-x-hidden">
                    <svg class="mr-1 w-3 h-3" fill="currentColor" viewBox="0 0 20 20"
                        xmlns="http://www.w3.org/2000/svg">
                        <path
                            d="M2 6a2 2 0 012-2h6a2 2 0 012 2v8a2 2 0 01-2 2H4a2 2 0 01-2-2V6zM14.553 7.106A1 1 0 0014 8v4a1 1 0 00.553.894l2 1A1 1 0 0018 13V7a1 1 0 00-1.447-.894l-2 1z">
                        </path>
                    </svg>
                    {{ item.categories }}
                </span>
                <span class="text-xs font-semibold italic text-blue-500">{{ item.update_date }}</span>
            </div>
            <h2 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{{ item.title}}</h2>
            <p class="mb-5 font-light text-gray-600 dark:text-gray-400 max-h-[100px] overflow-hidden">{{ item.abstract }}</p>
            <div class="flex justify-between items-center">
                <div class="text-sm flex items-center text-blue-700 dark:text-blue-500">
                    <svg class="w-4 h-4 mr-2 text-gray-800 dark:text-white" aria-hidden="true"
                        xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 18 20">
                        <path stroke="#323ea8" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="M4 4H1m3 4H1m3 4H1m3 4H1m6.071.286a3.429 3.429 0 1 1 6.858 0M4 1h12a1 1 0 0 1 1 1v16a1 1 0 0 1-1 1H4a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1Zm9 6.5a2.5 2.5 0 1 1-5 0 2.5 2.5 0 0 1 5 0Z" />
                    </svg>
                    <p class="font-medium">{{ item.submitter }}</p>
                </div>
                <button type="submit" @click="seePaperDetails(item)"
                    class="text-white inline-flex items-center font-medium rounded-xl h-[95%] rounded-md bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium text-sm px-6 py-2.5 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Pročitaj
                    više <svg class="ml-2 w-4 h-4" fill="currentColor" viewBox="0 0 20 20"
                        xmlns="http://www.w3.org/2000/svg">
                        <path fill-rule="evenodd"
                            d="M10.293 3.293a1 1 0 011.414 0l6 6a1 1 0 010 1.414l-6 6a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-4.293-4.293a1 1 0 010-1.414z"
                            clip-rule="evenodd"></path>
                    </svg></button>
            </div>
        </article>
    </div>

    <!-- Main modal -->
    <div v-if="paperDialog" tabindex="-1" aria-hidden="true"
        class="overflow-y-auto overflow-x-hidden fixed flex z-50 justify-center items-center bg-black bg-opacity-50 w-full inset-0 max-h-full">
        <div class="relative p-4 w-full max-w-2xl max-h-full">
            <!-- Modal content -->
            <div class="relative bg-white rounded-lg shadow dark:bg-gray-700">
                <!-- Modal header -->
                <div class="flex items-center justify-between p-4 md:p-5 border-b rounded-t dark:border-gray-600">
                    <h3 class="text-xl font-bold plus-jakarta-sans text-gray-900 dark:text-white">
                        Detalji znanstvenog rada
                    </h3>
                    <button type="button" @click="paperDialog = false"
                        class="text-gray-400 bg-transparent hover:bg-gray-200 hover:text-gray-900 rounded-lg text-sm w-8 h-8 ms-auto inline-flex justify-center items-center dark:hover:bg-gray-600 dark:hover:text-white"
                        data-modal-hide="default-modal">
                        <svg class="w-3 h-3" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none"
                            viewBox="0 0 14 14">
                            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                d="m1 1 6 6m0 0 6 6M7 7l6-6M7 7l-6 6" />
                        </svg>
                        <span class="sr-only">Close modal</span>
                    </button>
                </div>
                <!-- Modal body -->
                <div class="py-4 md:py-5 space-y-4 px-5 md:px-7">
                    <div class="flex justify-between items-center mb-5 text-gray-500">
                        <span
                            class="bg-blue-100 text-blue-500 text-xs font-medium inline-flex items-center px-2.5 py-0.5 rounded dark:bg-blue-600 max-w-[50%] dark:text-white overflow-x-hidden">
                            <svg class="mr-1 w-3 h-3" fill="currentColor" viewBox="0 0 20 20"
                                xmlns="http://www.w3.org/2000/svg">
                                <path
                                    d="M2 6a2 2 0 012-2h6a2 2 0 012 2v8a2 2 0 01-2 2H4a2 2 0 01-2-2V6zM14.553 7.106A1 1 0 0014 8v4a1 1 0 00.553.894l2 1A1 1 0 0018 13V7a1 1 0 00-1.447-.894l-2 1z">
                                </path>
                            </svg>
                            {{ paper.categories }}
                        </span>
                        <span class="text-sm font-semibold italic text-blue-500">Objavljeno {{ paper.year }}. godine</span>
                    </div>
                    <h2
                        class="mb-2 text-2xl font-bold tracking-tight dark:text-white text-center text-blue-500 plus-jakarta-sans">
                        {{ paper.title }}</h2>
                    <p
                        class="text-base leading-relaxed text-gray-500 dark:text-white pt-2 plus-jakarta-sans-regular max-h-[50vh] overflow-y-auto" v-html="paper.abstract">
                    </p>
                    <div class="flex justify-between items-center mb-5 text-gray-500">
                        <span class="text-sm font-semibold italic text-blue-500"><span class="font-bold">Autori:</span> {{ paper.authors }}</span>
                    </div>
                </div>
                <!-- Modal footer -->
                <div class="flex items-center justify-end p-4 md:p-5 border-t border-gray-200 rounded-b dark:border-gray-600">
                    <button type="button" @click="paperDialog = false"
                        class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Zatvori</button>
                </div>
            </div>
        </div>
    </div>

    <div class="mx-2 flex justify-center mt-10 mb-2 text-gray-600 plus-jakarta-sans dark:text-white text-md">Trenutna stranica: {{ page }}</div>

    <div class="flex justify-center items-center">
        <button @click="page--" :disabled="page === 1"
            class="text-blue-700 mr-2 flex items-center dark:text-blue-500 bg-blue-100 dark:bg-blue-600 hover:bg-blue-200 dark:hover:bg-blue-700 dark:text-white focus:outline-none focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5">
            <svg class="w-3.5 h-3.5 me-2 rtl:rotate-180" aria-hidden="true" xmlns="http://www.w3.org/2000/svg"
                fill="none" viewBox="0 0 14 10">
                <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="M13 5H1m0 0 4 4M1 5l4-4" />
            </svg>
            <span>Prethodna</span>
        </button>
        <button @click="page++" :disabled="page * perPage >= props.items.length"
            class="text-blue-700 flex items-center dark:text-blue-500 bg-blue-100 dark:bg-blue-600 hover:bg-blue-200 dark:hover:bg-blue-700 dark:text-white focus:outline-none focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5">
            <span>Sljedeća</span>
            <svg class="w-3.5 h-3.5 ms-2 rtl:rotate-180" aria-hidden="true" xmlns="http://www.w3.org/2000/svg"
                fill="none" viewBox="0 0 14 10">
                <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="M1 5h12m0 0L9 1m4 4L9 9" />
            </svg>
        </button>
    </div>
</template>