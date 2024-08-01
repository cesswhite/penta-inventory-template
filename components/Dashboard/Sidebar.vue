<template>
    <div class="w-full h-full p-4">
        <div class="size-8 ml-3">
            <AppLogo />
        </div>
        <nav class="w-full mt-12">
            <ul class="flex flex-col gap-1">
                <li class="w-full h-auto">
                    <UButton to="/dashboard" icon="i-heroicons-home" size="lg" color="white" variant="ghost">
                        Dashboard
                    </UButton>
                </li>
                <li class="w-full h-auto">
                    <UButton to="/products" icon="i-heroicons-clipboard-document-check" size="lg" color="white"
                        variant="ghost">
                        Products
                    </UButton>
                </li>

            </ul>
        </nav>
    </div>
</template>

<script setup lang="ts">

</script>

<style scoped></style>