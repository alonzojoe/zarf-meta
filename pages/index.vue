<template>
    <div>
        <MainLayout>
            <div id="IndexPage" class="w-full overflow-auto">
                <div class="mx-auto max-w-[500px] overflow-hidden">
                    <div id="Posts" class="px-4 max-w-[600px] mx-auto">

                        <div v-if="isPosts" v-for="post in posts" :key="post">
                            <Post :post="post" @isDeleted="posts = []" />
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
let isPosts = ref(true)
let isLoading = ref(false)

watchEffect(() => {
    if (!user.value) {
        // console.log('user', user.value)
        return navigateTo('/auth')
    }
})

onBeforeMount(() => {
    posts.value = [
        {
            name: 'Joe Alonzo',
            image: 'https://placehold.co/100',
            text: 'This is the title',
            picture: 'https://placehold.co/500',
        },
        {
            name: 'Joe Alonzo',
            image: 'https://placehold.co/100',
            text: 'This is the title',
            picture: 'https://placehold.co/500',
        },
        {
            name: 'Joe Alonzo',
            image: 'https://placehold.co/100',
            text: 'This is the title',
            picture: 'https://placehold.co/500',
        },
        {
            name: 'Joe Alonzo',
            image: 'https://placehold.co/100',
            text: 'This is the title',
            picture: 'https://placehold.co/500',
        },
        {
            name: 'Joe Alonzo',
            image: 'https://placehold.co/100',
            text: 'This is the title',
            picture: 'https://placehold.co/500',
        },
        {
            name: 'Joe Alonzo',
            image: 'https://placehold.co/100',
            text: 'This is the title',
            picture: 'https://placehold.co/500',
        }
    ]
})

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
