<template>
    <div class="w-full relative grid grid-cols-12 gap-1 p-1 bg-gray-100 h-dvh ? overflow-hidden">
        <div class="col-span-2 h-auto border border-gray-200 bg-zinc-50 rounded-xl">
            <DashboardSidebar />
        </div>
        <div class="col-span-10 h-full border border-gray-200 bg-zinc-50 rounded-xl p-4">
            <slot />
        </div>
    </div>
</template>

<script setup lang="ts">
useSeoMeta({
    title: 'Penta | Dashboard'
})
</script>
