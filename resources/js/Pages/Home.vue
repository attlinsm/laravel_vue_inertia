<script setup>
import { Head, Link } from '@inertiajs/vue3';
import Navbar from "@/Components/body/Navbar.vue";
import SideMenu from "@/Components/body/SideMenu.vue";
import Main from "@/Components/body/Main.vue";

defineProps({
    canLogin: Boolean,
    canRegister: Boolean,
    menuIsOpen: Boolean,
});


</script>

<template>

    <Head title="TaskManager" />
    <div class="min-h-screen">

        <div class="flex flex-col justify-between bg-navs">

            <Navbar
                :canLogin="canLogin"
                :canRegister="canRegister"
                @update:menuIsOpen="menuIsOpen = $event">
            </Navbar>

        </div>

        <div class="flex flex-row min-h-screen bg-navs flex-wrap">

            <SideMenu
                :menuIsOpen ="menuIsOpen">
            </SideMenu>

            <Main>

            </Main>

        </div>

    </div>


</template>

<style>
.bg-dots-darker {
    background-image: url("data:image/svg+xml,%3Csvg width='30' height='30' viewBox='0 0 30 30' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M1.22676 0C1.91374 0 2.45351 0.539773 2.45351 1.22676C2.45351 1.91374 1.91374 2.45351 1.22676 2.45351C0.539773 2.45351 0 1.91374 0 1.22676C0 0.539773 0.539773 0 1.22676 0Z' fill='rgba(0,0,0,0.07)'/%3E%3C/svg%3E");
}
@media (prefers-color-scheme: dark) {
    .dark\:bg-dots-lighter {
        background-image: url("data:image/svg+xml,%3Csvg width='30' height='30' viewBox='0 0 30 30' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M1.22676 0C1.91374 0 2.45351 0.539773 2.45351 1.22676C2.45351 1.91374 1.91374 2.45351 1.22676 2.45351C0.539773 2.45351 0 1.91374 0 1.22676C0 0.539773 0.539773 0 1.22676 0Z' fill='rgba(255,255,255,0.07)'/%3E%3C/svg%3E");
    }
}
</style>
