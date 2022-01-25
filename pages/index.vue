<template>
    <div>
        <div class="text-center py-10">
            <h1 class="text-4xl font-bold">Anúncios</h1>
        </div>
        <div class="mt-2">
            <anuncio
                v-for="anuncio in anuncios"
                :key="anuncio.id"
                :anuncio="anuncio"
            />
        </div>
    </div>
</template>

<script>
import ALL_ANUNCIOS from "@/graphql/AllAnuncios.gql";
export default {
    apollo: {
        anuncios: {
            query: ALL_ANUNCIOS,
            fetchPolicy: "network-only",
        },
    },
};
</script>
