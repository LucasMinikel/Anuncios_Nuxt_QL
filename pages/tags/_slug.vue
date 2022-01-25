<template>
    <div>
        <div class="text-center py-10" v-if="tag">
            <h1 class="text-4xl font-bold">{{ tag.titulo }} anúncios</h1>
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
import ALL_ANUNCIOS_BY_TAG from "@/graphql/AllAnunciosByTag.gql";
import TAG_BY_SLUG from "@/graphql/TagBySlug.gql";
export default {
    apollo: {
        tag: {
            variables() {
                return {
                    slug: this.$route.params.slug,
                };
            },
            query: TAG_BY_SLUG,
        },
        anuncios: {
            variables() {
                return {
                    slug: this.$route.params.slug,
                };
            },
            query: ALL_ANUNCIOS_BY_TAG,
        },
    },
};
</script>