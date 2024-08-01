<template>
    <UContainer>
        <UCard class="mt-10">
            <template #header>
                <div class="flex justify-between">
                    <h1>Welcome to Nuxt UI Starter</h1>
                    <ColorScheme>
                        <USelect v-model="$colorMode.preference" :options="['system', 'light', 'dark']" />
                    </ColorScheme>
                </div>
            </template>
            <UButton icon="i-heroicons-book-open" to="https://ui.nuxt.com" target="_blank">Open Nuxt UI Documentation
            </UButton>
        </UCard>
    </UContainer>
</template>


<script setup lang="ts">
const supabase = useSupabaseClient()

const signInWithOAuth = async () => {
    const { error } = await supabase.auth.signInWithOAuth({
        provider: 'github',
        options: {
            redirectTo: 'http://localhost:3000/confirm',
        },
    })
    if (error) console.log(error)
}

const signOut = async () => {
    const { error } = await supabase.auth.signOut()
    if (error) console.log(error)
}
</script>
