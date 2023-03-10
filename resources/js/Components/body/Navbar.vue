<script setup>
import {onMounted, onUnmounted, ref} from "vue";
import {usePage} from "@inertiajs/vue3";


defineProps({
    canLogin: Boolean,
    canRegister: Boolean,
});

const open = ref(false);
const sideMenu = ref(false);
const user = usePage().props.auth.user;

onMounted(() => document.addEventListener('keydown', closeOnEscape));
onUnmounted(() => document.removeEventListener('keydown', closeOnEscape));

const closeOnEscape = (e) => {
    if (open.value && e.key === 'Escape') {
        open.value = false;
    }
    if (sideMenu.value && e.key === 'Escape') {
        sideMenu.value = false;
    }
};

</script>

<template>

    <nav class="bg-navs px-1 py-1 border-b border-zinc-900 border-transparent drop-shadow-md">

        <div class="flex flex-row justify-between py-1 px-1 mx-auto md:container items-center">

            <div>
                <button v-if="user" @click="$emit('update:sideMenu', !sideMenu); sideMenu = !sideMenu;" id="button" class="inline-flex items-center justify-center p-2 text-gray-400 hover:text-white">

                    <span class="sr-only">Открыть главное меню</span>

                    <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true">
                        <path v-if="!sideMenu" stroke-linecap="round" stroke-linejoin="round" d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5" />
                        <path v-if="sideMenu" stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                    </svg>

                </button>
            </div>

            <div class="inline-flex">

                <button class="p-2 text-gray-400 hover:text-white">

                    <span class="sr-only">Уведомления</span>
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M14.857 17.082a23.848 23.848 0 005.454-1.31A8.967 8.967 0 0118 9.75v-.7V9A6 6 0 006 9v.75a8.967 8.967 0 01-2.312 6.022c1.733.64 3.56 1.085 5.455 1.31m5.714 0a24.255 24.255 0 01-5.714 0m5.714 0a3 3 0 11-5.714 0" />
                    </svg>

                </button>

                <button @click="open = !open" class="p-2 text-gray-400 hover:text-white">

                    <span class="sr-only">Открыть опции пользователя</span>

                    <svg class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
                        <path v-if="!open" stroke-linecap="round" stroke-linejoin="round" d="M9.594 3.94c.09-.542.56-.94 1.11-.94h2.593c.55 0 1.02.398 1.11.94l.213 1.281c.063.374.313.686.645.87.074.04.147.083.22.127.324.196.72.257 1.075.124l1.217-.456a1.125 1.125 0 011.37.49l1.296 2.247a1.125 1.125 0 01-.26 1.431l-1.003.827c-.293.24-.438.613-.431.992a6.759 6.759 0 010 .255c-.007.378.138.75.43.99l1.005.828c.424.35.534.954.26 1.43l-1.298 2.247a1.125 1.125 0 01-1.369.491l-1.217-.456c-.355-.133-.75-.072-1.076.124a6.57 6.57 0 01-.22.128c-.331.183-.581.495-.644.869l-.213 1.28c-.09.543-.56.941-1.11.941h-2.594c-.55 0-1.02-.398-1.11-.94l-.213-1.281c-.062-.374-.312-.686-.644-.87a6.52 6.52 0 01-.22-.127c-.325-.196-.72-.257-1.076-.124l-1.217.456a1.125 1.125 0 01-1.369-.49l-1.297-2.247a1.125 1.125 0 01.26-1.431l1.004-.827c.292-.24.437-.613.43-.992a6.932 6.932 0 010-.255c.007-.378-.138-.75-.43-.99l-1.004-.828a1.125 1.125 0 01-.26-1.43l1.297-2.247a1.125 1.125 0 011.37-.491l1.216.456c.356.133.751.072 1.076-.124.072-.044.146-.087.22-.128.332-.183.582-.495.644-.869l.214-1.281z" />
                        <path v-if="!open" stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                        <path v-if="open" stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                    </svg>

                </button>
            </div>

        </div>

    </nav>

    <div v-show="open" class="fixed inset-0 z-40" @click="open = false"></div>
    <div v-show="sideMenu" class="fixed inset-0 z-40" @click="$emit('update:sideMenu', sideMenu = false)"></div>
    <transition
        appear
        enter-active-class="transition duration-400"
        enter-from-class="transform opacity-0 -translate-y-5"
        enter-to-class="transform opacity-100"
        leave-active-class="transition duration-400"
        leave-from-class="transform opacity-100"
        leave-to-class="transform opacity-0 -translate-y-5"
    >
        <div v-if="open"
             :class="{ block: open, hidden: !open  }"
             class="px-4 py-4 bg-navs md:absolute right-0 top-[70px] drop-shadow-md z-50"
             id="menu">
            <div v-if="!user">
                <a v-if="canRegister"
                   :href="route('register')"
                   class="mt-1 px-5 py-2 block text-white text-center hover:bg-gray-700 rounded duration-75">Регистрация</a>
                <a v-if="canLogin"
                   :href="route('login')"
                   class="mt-1 px-5 py-2 block text-white text-center hover:bg-gray-700 rounded duration-75">Авторизация</a>
            </div>
            <div v-if="user">
                <a :href="route('home')"
                   class="mt-1 px-5 py-2 block text-white text-center hover:bg-gray-700 rounded duration-75">Главная</a>
                <a :href="route('profile.edit')"
                   class="mt-1 px-5 py-2 block text-white text-center hover:bg-gray-700 rounded duration-75"> Профиль </a>
                <a :href="route('logout')"
                   class="mt-1 px-5 py-2 block text-white text-center hover:bg-gray-700 rounded duration-75"> Выход </a>
            </div>
        </div>
    </transition>
</template>
