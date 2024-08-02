<template>
    <div class="w-full flex flex-col">
        <div class="w-full flex items-center justify-between">
            <h2 class="text-3xl font-bold text-primary-950 rounded-lg ">
                Products
            </h2>
            <div class="w-auto">
                <UButton @click="openAddProductSlide = true" icon="i-heroicons-plus">
                    Add product
                </UButton>
            </div>
        </div>
        <div class="mt-12">
            <ProductsTable />
        </div>
        <USlideover v-model="openAddProductSlide" :ui="{
                    base: 'relative flex-1 flex flex-col w-full focus:outline-none rounded-l-2xl',
                }">
            <div class="p-4">
                <ProductsAddForm @done="openAddProductSlide = false" />
            </div>
        </USlideover>
    </div>
</template>

<script setup lang="ts">
const openAddProductSlide = ref(false)
</script>