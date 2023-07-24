<template>
    <div>
        <MainLayout>
            <div id="IndexPage" class="w-full overflow-auto">
                <div class="mx-auto max-w-[500px] overflow-auto">
                    <div id="Posts" class="px-4 max-w-[600px] mx-auto">

                        <div 
                            class="text-white" 
                            v-if="isPosts" v-for="post in posts" 
                            :key="post"
                        >
                            {{ post }}
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

    const useStore = useUserStore()

    let posts = ref([])
    let isPosts = ref(true)
    let isLoading = ref(false)

    onBeforeMount(() => {
        posts.value = [
            {
                name: 'Joe Alonzo',
                profile: 'https://placehold.co/100',
                text: 'This is the title',
                picture: 'https://placehold.co/500',
            }
        ]
    })

</script>
