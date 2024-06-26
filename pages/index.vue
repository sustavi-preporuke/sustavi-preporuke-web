<script setup>
import { initFlowbite } from 'flowbite'
import ArticleCard from '~/components/ArticleCard.vue';

useHead({
    title: 'Znanstveni Radovi',
    meta: [
        {
            name: 'description',
            content: 'Sustav preporuke znanstvenih radova'
        },
        {
            name: 'keywords',
            content: 'znanstveni radovi, preporuka, sustav'
        }
    ]
})

onMounted(() => {
    initFlowbite();
})

const search_term = ref('');
const papers = ref([]);
const loading = ref(false);

async function fetchData() {
    loading.value = true;
    try {
        const response = await useFetch('http://127.0.0.1:5000/recommend', {
            method: 'POST',
            body: {
                search_term: search_term.value,
            },
        })
        papers.value = response.data.value

    } catch (error) {
        console.error('Error fetching data:', error)
    }
    loading.value = false;
};
</script>

<template>
    <div class="bg-white dark:bg-gray-900 min-h-[100vh]">
        <section class="bg-gray-100 dark:bg-gray-800">
            <div class="grid max-w-screen-xl px-4 py-8 mx-auto md:gap-8 xl:gap-0 lg:py-16 md:grid-cols-12">
                <div class="mr-auto place-self-center md:col-span-7 md:pl-10">
                    <h1
                        class="max-w-2xl mb-4 text-3xl font-bold leading-none lg:text-5xl dark:text-white text-center md:text-left plus-jakarta-sans">
                        Sustav
                        preporuke znanstvenih radova</h1>
                    <p
                        class="max-w-2xl mb-6 text-gray-500 lg:mb-8 md:text-lg lg:text-lg dark:text-gray-400 text-center md:text-left plus-jakarta-sans">
                        Sustav za
                        preporuku znanstvenih radova je platforma koja korisnicima daje personalizirane prijedloge
                        znanstvenih
                        radova
                        na temelju
                        njihovih interesa i preferencija.</p>
                </div>
                <div class="flex mx-auto lg:mt-0 md:col-span-5 max-w-[70vw] md:max-w-[100vw] mb-10 mt-5">
                    <img src="/img/landing.png">
                </div>
            </div>
        </section>

        <div class="mx-auto md:max-w-[70%] max-w-[90%] mx-auto -mt-7 md:-mt-9 shadow-xl mb-10 dark:bg-gray-900">
            <label for="search" class="mb-2 text-sm font-medium text-gray-900 sr-only dark:text-white">Search</label>
            <div class="relative">
                <div class="absolute inset-y-0 start-2 md:start-4 flex items-center ps-3 py-5 pointer-events-none">
                    <svg class="w-5 h-5 text-gray-500 dark:text-gray-400" aria-hidden="true"
                        xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20">
                        <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z" />
                    </svg>
                </div>
                <input type="search" v-model="search_term" id="search_bar"
                    class="block w-full plus-jakarta-sans-regular py-3 md:py-5 pl-[15%] md:pl-[7%] text-md text-gray-900 border border-gray-300 rounded-sm bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                    placeholder="Unesite naziv teme" required />
                <button @click="fetchData"
                    class="text-white plus-jakarta-sans-regular absolute inset-y-1 end-1 bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-sm text-sm px-6 py-2 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
                    <svg aria-hidden="true" role="status" class="inline w-5 h-5 mr-3 mb-1 text-white animate-spin"
                        v-if="loading" viewBox="0 0 100 101" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path
                            d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z"
                            fill="#E5E7EB" />
                        <path
                            d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z"
                            fill="currentColor" />
                    </svg>
                    <span>Pretraži</span>
                </button>
            </div>
        </div>

        <div v-if="papers.length == 0" class="bg-white dark:bg-gray-900 px-7">
            <div class="mx-auto max-w-screen-sm text-center bg-white dark:bg-gray-900 pb-7">
                <h2
                    class="text-2xl md:text-3xl tracking-tight font-extrabold text-gray-900 dark:text-white pb-4 plus-jakarta-sans-semibold">
                    Unesite naziv teme
                    kako biste pregledali radove</h2>
                <div class="h-2 w-[10%] bg-blue-600 mx-auto rounded-lg"></div>
            </div>
        </div>

        <div class="mx-auto" v-else>
            <section class="bg-white dark:bg-gray-900">
                <div class="py-5 px-4 mx-auto max-w-screen-xl lg:py-10 lg:px-6">
                    <div class="mx-auto max-w-screen-sm text-center lg:mb-16 mb-8 plus-jakarta-sans-semibold">
                        <h2 class="text-3xl lg:text-4xl tracking-tight font-extrabold text-gray-900 dark:text-white">
                            Preporučeni
                            radovi</h2>
                        <div class="h-2 w-[10%] bg-blue-600 mx-auto rounded-lg mt-4 mb-3"></div>
                        <p class="font-light text-gray-00 sm:text-xl dark:text-gray-400">Prikaz znanstvenih radova za
                            temu: <span class="font-semibold text-blue-600 capitalize">{{ search_term }}</span></p>
                    </div>
                    <div>
                        <ArticleCard :items="papers"></ArticleCard>
                    </div>
                </div>
            </section>
        </div>
    </div>
</template>

<style scoped>
#search_bar {
    -webkit-appearance: none;
    appearance: none;
}
</style>
