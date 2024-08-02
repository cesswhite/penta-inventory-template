<template>
    <div>
        <div class="flex px-3 py-3.5 border-b border-gray-200 dark:border-gray-700">
            <UInput v-model="search_product" placeholder="Filter products..." />
        </div>
        <UTable :rows="filteredRows" :columns="columns" />
    </div>
</template>


<script setup lang="ts">
import type { Product } from '~/types/products';
const columns = [{
    key: 'id',
    label: 'ID'
}, {
    key: 'name',
    label: 'Name'
}, {
    key: 'title',
    label: 'Title'
}, {
    key: 'email',
    label: 'Email'
}, {
    key: 'role',
    label: 'Role'
}]

const people = [{
    id: 1,
    name: 'Lindsay Walton',
    title: 'Front-end Developer',
    email: 'lindsay.walton@example.com',
    role: 'Member'
}, {
    id: 2,
    name: 'Courtney Henry',
    title: 'Designer',
    email: 'courtney.henry@example.com',
    role: 'Admin'
}, {
    id: 3,
    name: 'Tom Cook',
    title: 'Director of Product',
    email: 'tom.cook@example.com',
    role: 'Member'
}, {
    id: 4,
    name: 'Whitney Francis',
    title: 'Copywriter',
    email: 'whitney.francis@example.com',
    role: 'Admin'
}, {
    id: 5,
    name: 'Leonard Krasner',
    title: 'Senior Designer',
    email: 'leonard.krasner@example.com',
    role: 'Owner'
}, {
    id: 6,
    name: 'Floyd Miles',
    title: 'Principal Designer',
    email: 'floyd.miles@example.com',
    role: 'Member'
}]

const search_product = ref('')
const all_products = ref<Product[] | null>(null)

onMounted(async() => {

})

const filteredRows = computed(() => {
    if (!search_product.value) {
        return all_products.value
    }
    if (all_products.value) {
        return all_products.value.filter((product: Product) => {
            return Object.values(product).some((value) => {
                return String(value).toLowerCase().includes(search_product.value.toLowerCase())
            })
        })
    }
})

async function getAllProducts(){
    
}
</script>
