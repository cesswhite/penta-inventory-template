<template>
    <div id="auth-sign-in" class="w-full h-auto relative">
        <div class="flex flex-col gap-4 items-center justify-center mb-12">
            <div class="size-8">
                <AppLogo />
            </div>
            <div class="flex items-center justify-center flex-col gap-0">
                <span class="text-2xl font-bold text-primary-950">
                    Sign In
                </span>
                <p class="text-sm text-primary-950/60">
                    Please insert your email and password to continue
                </p>
            </div>
        </div>
        <UForm :validate="validate" :state="state" class="space-y-4" @submit="signInWithOtp">
            <UFormGroup label="Email" name="email" size="lg">
                <UInput v-model="state.email" color="gray" variant="outline" />
            </UFormGroup>

            <UFormGroup label="Password" name="password" size="lg">
                <UInput v-model="state.password" type="password" color="gray" variant="outline" />
            </UFormGroup>

            <UButton block type="submit" size="lg" :loading="loading">
                Submit
            </UButton>
        </UForm>
    </div>
</template>

<script setup lang="ts">
import type { Database } from '~/types'
import type { FormError, FormSubmitEvent } from '#ui/types'
const client = useSupabaseClient<Database>()
const toast = useToast()
const loading = ref(false)
const state = reactive({
    email: undefined,
    password: undefined
})

const validate = (state: any): FormError[] => {
    const errors = []
    if (!state.email) errors.push({ path: 'email', message: 'Required' })
    if (!state.password) errors.push({ path: 'password', message: 'Required' })
    return errors
}

const signInWithOtp = async () => {
    if (state.email && state.password) {
        loading.value = true
        try {
            const { data, error } = await client.auth.signInWithPassword({
                email: state.email,
                password: state.password
            })
            if (error) {
                toast.add({
                    title: 'Error',
                    description: error?.message,
                    color: 'red'
                })
            } else {
                navigateTo('/dashboard')
            }
            loading.value = false
        } catch (error) {
            console.error(error)
        }
    }
}
</script>
