<template>
    <div>
        <div class="text-center py-10">
            <h1 class="text-4xl font-bold mb-2">
                Encontre os melhores anúncios
            </h1>
            <p class="text-gray-600 font-medium">Para você</p>
        </div>
        <div class="mt-10">
            <anuncio
                v-for="anuncio in anuncios"
                :key="anuncio.id"
                :anuncio="anuncio"
            />
        </div>
    </div>
</template>

<script>
import gql from "graphql-tag";
export default {
    apollo: {
        anuncios: {
            query: gql`
                {
                    anuncios(orderBy: [{ column: CREATED_AT, order: DESC }]) {
                        id
                        anuncio_titulo
                        anuncio_local
                        anuncio_link
                        anuncio_empresa
                        anuncio_logo
                        tags {
                            titulo
                            slug
                        }
                    }
                }
            `,
            fetchPolicy: "network-only",
        },
    },
};
</script>
