<template>
    <header class="py-6 flex items-center justify-between">
        <nuxt-link :to="{ name: 'index' }" exact-active-class="text-blue-500"
            >Anúncios</nuxt-link
        >
        <div class="-mx-4 flex items-center flex-wrap">
            <span class="mx-4 font-bold">Alex</span>
            <nuxt-link
                :to="{ name: 'login' }"
                class="mx-4"
                exact-active-class="text-blue-500"
                >Entrar</nuxt-link
            >
            <a href="" class="mx-4" exact-active-class="text-blue-500">Sair</a>
            <a href="" class="mx-4" exact-active-class="text-blue-500"
                >Gerenciador</a
            >
            <a href="" class="mx-4" exact-active-class="text-blue-500"
                >Criar anúncio</a
            >
        </div>
    </header>
</template>