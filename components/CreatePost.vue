<template>
    <div id="CreatePost" class="fixed z-50 bottom-0 w-full overflow-hidden">

    </div>
</template>

<script setup>
import { useUserStore } from '../stores/user';
const useStore = useUserStore()

const runtimeConfig = useRuntimeConfig()
let isMenu = ref(false)
let isLike = ref(false)
let isDeleting = ref(false)

const emits = defineEmits(['isDeleted'])
const props = defineProps({ post: Object })

// const client = useSupabaseClient()
// const user = useSupabaseUser()
</script>
