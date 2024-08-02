<template>
    <div id="auth-sign-in" class="w-full h-auto relative">
        <div class="flex items-start justify-center flex-col gap-0 mb-8">
            <span class="text-2xl font-bold text-primary-950">
                Add product
            </span>
            <p class="text-sm text-primary-950/60">
                Please fill in the details below to add a new product to the inventory.
            </p>
        </div>
        <UForm :validate="validate" :state="state" class="space-y-4" @submit="addProduct">
            <UFormGroup label="Name" name="name" size="lg">
                <UInput v-model="state.name" color="gray" variant="outline" />
            </UFormGroup>

            <UFormGroup label="Description" name="description" size="lg">
                <UInput v-model="state.description" color="gray" variant="outline" />
            </UFormGroup>

            <UFormGroup label="SKU" name="sku" size="lg">
                <UInput v-model="state.sku" color="gray" variant="outline" />
            </UFormGroup>

            <UFormGroup label="Category" name="category" size="lg">
                <UInput v-model="state.category" color="gray" variant="outline" />
            </UFormGroup>

            <UFormGroup label="Price" name="price" size="lg">
                <UInput v-model="state.price" type="number" color="gray" variant="outline" />
            </UFormGroup>

            <UFormGroup label="Quantity" name="quantity" size="lg">
                <UInput v-model="state.quantity" type="number" color="gray" variant="outline" />
            </UFormGroup>

            <UFormGroup label="Provider" name="provider" size="lg">
                <UInput v-model="state.provider" color="gray" variant="outline" />
            </UFormGroup>

            <UButton block type="submit" size="lg" :loading="loading">
                Save product
            </UButton>
        </UForm>

    </div>
</template>

<script setup lang="ts">
import type { Database } from '~/types'
import type { FormError, FormSubmitEvent } from '#ui/types'

const emit = defineEmits(['done'])
const client = useSupabaseClient<Database>()
const toast = useToast()
const loading = ref(false)
const state = reactive({
    name: undefined,
    description: undefined,
    sku: undefined,
    category: undefined,
    price: undefined,
    quantity: undefined,
    provider: undefined,
})

const validate = (state: any): FormError[] => {
    const errors = []
    if (!state.name) errors.push({ path: 'name', message: 'Name is required' })
    if (!state.description) errors.push({ path: 'description', message: 'Description is required' })
    if (!state.sku) errors.push({ path: 'sku', message: 'SKU is required' })
    if (!state.category) errors.push({ path: 'category', message: 'Category is required' })
    if (!state.price) errors.push({ path: 'price', message: 'Price is required' })
    if (!state.quantity) errors.push({ path: 'quantity', message: 'Quantity is required' })
    if (!state.provider) errors.push({ path: 'provider', message: 'Provider is required' })
    return errors
}

const addProduct = async () => {
    loading.value = true
    try {
        const { data, error } = await client.from('penta_products').insert([
            {
                name: state.name,
                description: state.description,
                sku: state.sku,
                category: state.category,
                price: state.price,
                quantity: state.quantity,
                provider: state.provider,
            },
        ]).single();

        if (error) {
            toast.add({
                title: 'Error',
                description: error?.message,
                color: 'red'
            })
        } else {
            emit('done')
        }
        loading.value = false
    } catch (error) {
        console.error(error)
    }
}
</script>
