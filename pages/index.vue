<template>
    <div>
        <MainLayout>
            <div id="IndexPage" class="w-full overflow-auto">
                <div class="mx-auto max-w-[500px] overflow-hidden">
                    <div id="Posts" class="px-4 max-w-[600px] mx-auto">

                        <div v-if="isPosts" v-for="post in posts" :key="post">
                            <Post :post="post" @isDeleted="posts = []" />
                        </div>
                        <div v-else>
                            <client-only>
                                <div v-if="isLoading" class="mt-20 w-full flex items-center justify-center mx-auto">
                                    <div class="text-white mx-auto flex flex-col items-center justify-center">
                                        <Icon name="eos-icons:bubble-loading" size="50" color="#ffffff" />
                                        <div class="w-full mt-1">Loading...</div>
                                    </div>
                                </div>
                                <div v-else class="mt-20 w-full flex items-center justify-center mx-auto">
                                    <div class="text-white mx-auto flex flex-col items-center justify-center">
                                        <Icon name="tabler:mood-empty" size="50" color="#ffffff" />
                                        <div class="w-full mt-1">Make the first posts!</div>
                                    </div>
                                </div>
                            </client-only>
                        </div>

                    </div>
                </div>
            </div>
        </MainLayout>
    </div>
</template>

<script setup>
import MainLayout from '../layouts/MainLayout.vue'

import { useUserStore } from '../stores/user';
const userStore = useUserStore()
const user = useSupabaseUser()

let posts = ref([])
let isPosts = ref(false)
let isLoading = ref(false)

watchEffect(() => {
    if (!user.value) {
        return navigateTo('/auth')
    }
})

onBeforeMount(async () => {
    try {
        isLoading = true
        await userStore.getAllPosts()
        isLoading = false
    } catch (error) {
        console.log(error)
    }
    
})

onMounted(() => {
    if (userStore.posts && userStore.posts.length >= 1) {
        posts.value = userStore.posts
        isPosts.value = true
    }
})

watch(() => posts.value, () => { //call back function for mobile devices
    if (userStore.posts && userStore.posts.length >= 1) {
        posts.value = userStore.posts
        isPosts.value = true
    }
}, { deep: true })

</script>

<style scoped>
#IndexPage::-webkit-scrollbar {
    width: 0.5em;
}

#IndexPage::-webkit-scrollbar-track {
    background: transparent;
}

#IndexPage::-webkit-scrollbar-thumb {
    background-color: transparent;
}
</style>
