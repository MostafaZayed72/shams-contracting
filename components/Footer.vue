<template>
    <footer class=" text-white  bg-primary w-full ">
        <div class="w-full  flex flex-col-reverse gap-2 md:flex-row flex-wrap justify-between items-center">
            <!-- شعار الموقع -->
            <div class="flex items-center space-x-3 mx-4">
                <img src="/imgs/logo.png" alt="Site Logo" class="h-12 w-12 mx-2 rounded-full bg-white" />
                <span class="text-sm md:text-xl">
                    &copy; {{ new Date().getFullYear() }} {{ $t('All rights reserved to Shams.') }}
                </span>
            </div>
            <h1 class="my-auto">
                {{ $t('Mail Us') }} : <a href="mailto:support@example.com"
                    class="underline text-green-300 hover:text-green-400 delayed">Shams@gmail.com</a>
            </h1>
            <!-- الروابط -->
            <nav class="flex space-x-6 md:text-xl  mx-4">

                <nuxt-link to="/contact" class="hover:underline hover:text-green-300 mx-6 delayed">
                    {{ $t('Contact Us') }}
                </nuxt-link>
                <nuxt-link to="/about" class="hover:underline hover:text-green-300 delayed">
                    {{ $t('About Us') }}
                </nuxt-link>
                <!-- <nuxt-link to="/products" class="hover:underline hover:text-green-300 delayed">
                    {{ $t('Products') }}
                </nuxt-link> -->

            </nav>
        </div>
    </footer>
</template>

<script setup>
</script>

<style scoped></style>