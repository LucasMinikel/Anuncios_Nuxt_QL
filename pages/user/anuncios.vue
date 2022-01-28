<template>
    <div>
        <div class="text-center py-10">
            <h1 class="text-4xl font-bold">Seus Anúncios</h1>
        </div>
        <div class="mt-2" v-if="me">
            <anuncio
                v-for="anuncio in me.anuncios"
                :key="anuncio.id"
                :anuncio="anuncio"
            >
                <template slot="actions">
                    <nuxt-link
                        :to="{
                            name: 'anuncios-id-edit',
                            params: { id: anuncio.id },
                        }"
                        class="font-medium text-blue-500"
                        >Editar</nuxt-link
                    >
                </template>
            </anuncio>
        </div>
    </div>
</template>

<script>
import USER_ANUNCIOS from "@/graphql/UserAnuncios.gql";
export default {
    apollo: {
        me: {
            query: USER_ANUNCIOS,
            fetchPolicy: "network-only",
            prefetch: false,
        },
    },
};
</script>
