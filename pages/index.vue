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
import gql from "graphql-tag";
export default {
    apollo: {
        anuncios: {
            query: gql`
                {
                    anuncios(
                        orderBy: [
                            { column: CREATED_AT, order: DESC }
                            { column: ANUNCIO_FAVORITO, order: DESC }
                        ]
                    ) {
                        id
                        anuncio_titulo
                        anuncio_local
                        anuncio_link
                        anuncio_empresa
                        anuncio_logo
                        anuncio_marcado
                        anuncio_favorito
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
