<template>
    <header class="py-6 flex items-center justify-between">
        <nuxt-link :to="{ name: 'index' }" exact-active-class="text-blue-500"
            >Anúncios</nuxt-link
        >
        <div class="-mx-4 flex items-center flex-wrap">
            <template v-if="$auth.loggedIn">
                <div>
                    <span class="mx-4 font-bold">{{ $auth.user.name }}</span>
                    <a href="" class="mx-4" exact-active-class="text-blue-500"
                        >Criar anúncio</a
                    >
                    <a href="" class="mx-4" exact-active-class="text-blue-500"
                        >Gerenciador</a
                    >
                    <a href="" class="mx-4" exact-active-class="text-blue-500"
                        >Sair</a
                    >
                </div>
            </template>
            <template v-if="!$auth.loggedIn">
                <div>
                    <nuxt-link
                        :to="{ name: 'login' }"
                        class="mx-4"
                        exact-active-class="text-blue-500"
                        >Entrar</nuxt-link
                    >
                </div>
            </template>
        </div>
    </header>
</template>