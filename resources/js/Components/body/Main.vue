<script setup>
import {usePage} from "@inertiajs/vue3";

const user = usePage().props.auth.user;

</script>

<template>
    <main class="py-4 px-4 text-center text-white bg-main flex flex-col grow">

        <div v-if="!user" class="m-4 p-4 flex justify-center self-center max-w-sm border border-zinc-900 border-transparent drop-shadow-md bg-navs">
            <p>
                Авторизуйтесь, чтобы продолжить работу
            </p>
        </div>


        <div v-if="user" class="grid grid-cols-2 gap-4 mx-auto">
            <div class="max-w-xs p-4 border border-zinc-900 border-transparent drop-shadow-md bg-navs ">
                <p>
                    Title
                </p>
                <p>
                    Last update
                </p>
                <p>
                    New tasks
                </p>
                <p>
                    Description
                </p>
            </div>
            <div class="max-w-xs p-4 border border-zinc-900 border-transparent drop-shadow-md bg-navs ">
                <p>
                    Title
                </p>
                <p>
                    Last update
                </p>
                <p>
                    New tasks
                </p>
                <p>
                    Description
                </p>
            </div>
        </div>

    </main>
</template>
