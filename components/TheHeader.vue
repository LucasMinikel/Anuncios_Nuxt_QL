<template>
    <header class="py-6 flex items-center justify-between">
        <nuxt-link :to="{ name: 'index' }" exact-active-class="text-blue-500"
            >Anúncios</nuxt-link
        >
        <div class="-mx-4 flex items-center flex-wrap">
            <template v-if="$auth.loggedIn">
                <div>
                    <span class="mx-4 font-bold">{{ $auth.user.name }}</span>
                    <nuxt-link
                        :to="{ name: 'anuncios-create' }"
                        class="mx-4"
                        exact-active-class="text-blue-500"
                        >Criar anúncio</nuxt-link
                    >
                    <nuxt-link
                        :to="{ name: 'user-anuncios' }"
                        class="mx-4"
                        exact-active-class="text-blue-500"
                        >Meus anúncios</nuxt-link
                    >
                    <a
                        href=""
                        class="mx-4"
                        exact-active-class="text-blue-500"
                        @click.prevent="logout"
                        >Sair</a
                    >
                </div>
            </template>
            <template v-if="!$auth.loggedIn">
                <div>
                    <nuxt-link
                        :to="{ name: 'register' }"
                        class="mx-4"
                        exact-active-class="text-blue-500"
                        >Criar Conta</nuxt-link
                    >
                </div>
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
<script>
export default {
    methods: {
        async logout() {
            await this.$auth.logout();
            this.$router.replace({ name: "index" });
        },
    },
};
</script>
