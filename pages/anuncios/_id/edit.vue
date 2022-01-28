<template>
    <div class="mt-10 flex justify-center">
        <form action="" class="w-6/12" v-if="me" @submit.prevent="submit">
            <h2 class="mb-4 text-2xl font-bold">Editar anúncio</h2>
            <div class="mb-4">
                <label
                    for="anuncio_titulo"
                    class="inline-block mb-1 font-medium"
                    >Título</label
                >
                <input
                    type="anuncio_titulo"
                    name="anuncio_titulo"
                    id="anuncio_titulo"
                    class="
                        bg-gray-200
                        border-2 border-gray-200
                        rounded-lg
                        w-full
                        h-10
                        px-4
                    "
                    placeholder="Meu anúncio"
                    v-model="me.anuncios[0].anuncio_titulo"
                    :class="{ 'border-red-500': erros['input.anuncio_titulo'] }"
                />
                <div
                    class="text-sm text-red-500 mt-1"
                    v-if="erros['input.anuncio_titulo']"
                >
                    {{ erros["input.anuncio_titulo"][0] }}
                </div>
            </div>
            <div class="mb-4">
                <label for="anuncio_local" class="inline-block mb-1 font-medium"
                    >Local</label
                >
                <input
                    type="anuncio_local"
                    name="anuncio_local"
                    id="anuncio_local"
                    class="
                        bg-gray-200
                        border-2 border-gray-200
                        rounded-lg
                        w-full
                        h-10
                        px-4
                    "
                    placeholder="Rua tal"
                    v-model="me.anuncios[0].anuncio_local"
                    :class="{ 'border-red-500': erros['input.anuncio_local'] }"
                />
                <div
                    class="text-sm text-red-500 mt-1"
                    v-if="erros['input.anuncio_local']"
                >
                    {{ erros["input.anuncio_local"][0] }}
                </div>
            </div>
            <div class="mb-4">
                <label for="anuncio_link" class="inline-block mb-1 font-medium"
                    >Link</label
                >
                <input
                    type="anuncio_link"
                    name="anuncio_link"
                    id="anuncio_link"
                    class="
                        bg-gray-200
                        border-2 border-gray-200
                        rounded-lg
                        w-full
                        h-10
                        px-4
                    "
                    placeholder="Link do meu anúncio"
                    v-model="me.anuncios[0].anuncio_link"
                    :class="{ 'border-red-500': erros['input.anuncio_link'] }"
                />
                <div
                    class="text-sm text-red-500 mt-1"
                    v-if="erros['input.anuncio_link']"
                >
                    {{ erros["input.anuncio_link"][0] }}
                </div>
            </div>
            <div class="mb-4">
                <label for="tags" class="inline-block mb-1 font-medium"
                    >Tags</label
                >
                <v-select
                    inputId="tags"
                    :options="tags"
                    label="titulo"
                    multiple
                    v-model="me.anuncios[0].tags"
                    class="border-2 border-gray-200 rounded-lg bg-gray-200"
                    :class="{ 'border-red-500': erros['input.tags.sync'] }"
                ></v-select>
                <div
                    class="text-sm text-red-500 mt-1"
                    v-if="erros['input.tags.sync']"
                >
                    {{ erros["input.tags.sync"][0] }}
                </div>
            </div>
            <div class="mb-4">
                <label
                    for="anuncio_empresa"
                    class="inline-block mb-1 font-medium"
                    >Empresa</label
                >
                <input
                    type="anuncio_empresa"
                    name="anuncio_empresa"
                    id="anuncio_empresa"
                    class="
                        bg-gray-200
                        border-2 border-gray-200
                        rounded-lg
                        w-full
                        h-10
                        px-4
                    "
                    placeholder="Minha empresa"
                    v-model="me.anuncios[0].anuncio_empresa"
                    :class="{
                        'border-red-500': erros['input.anuncio_empresa'],
                    }"
                />
                <div
                    class="text-sm text-red-500 mt-1"
                    v-if="erros['input.anuncio_empresa']"
                >
                    {{ erros["input.anuncio_empresa"][0] }}
                </div>
            </div>
            <div class="mb-4">
                <label for="anuncio_logo" class="inline-block mb-1 font-medium"
                    >URL Logo</label
                >
                <input
                    type="anuncio_logo"
                    name="anuncio_logo"
                    id="anuncio_logo"
                    class="
                        bg-gray-200
                        border-2 border-gray-200
                        rounded-lg
                        w-full
                        h-10
                        px-4
                    "
                    placeholder="Minha empresa"
                    v-model="me.anuncios[0].anuncio_logo"
                    :class="{ 'border-red-500': erros['input.anuncio_logo'] }"
                />
                <div
                    class="text-sm text-red-500 mt-1"
                    v-if="erros['input.anuncio_logo']"
                >
                    {{ erros["input.anuncio_logo"][0] }}
                </div>
            </div>

            <div class="mb-4">
                <input
                    type="checkbox"
                    name="anuncio_marcado"
                    id="anuncio_marcado"
                    class="mr-2"
                    v-model="me.anuncios[0].anuncio_marcado"
                /><label for="anuncio_marcado">Marcado</label>
            </div>
            <div class="mb-4">
                <input
                    type="checkbox"
                    name="anuncio_favorito"
                    id="anuncio_favorito"
                    class="mr-2"
                    v-model="me.anuncios[0].anuncio_favorito"
                /><label for="anuncio_favorito">Favorito</label>
            </div>
            <button
                type="submit"
                class="p-4 bg-blue-500 text-white font-medium rounded-lg"
            >
                Salvar
            </button>
        </form>
    </div>
</template>


<script>
import USER_ANUNCIO_BY_ID from "@/graphql/UserAnuncioById.gql";
import ALL_TAGS from "@/graphql/AllTags.gql";
import UPDATE_ANUNCIO from "@/graphql/UpdateAnuncio.gql";
export default {
    data() {
        return {
            erros: {},
        };
    },
    computed: {
        tagsIds() {
            return this.me.anuncios[0].tags.map((t) => t.id);
        },
    },
    apollo: {
        me: {
            prefetch: false,
            query: USER_ANUNCIO_BY_ID,
            variables() {
                return {
                    id: this.$route.params.id,
                };
            },
        },
        tags: {
            query: ALL_TAGS,
        },
    },
    methods: {
        submit() {
            this.$apollo
                .mutate({
                    mutation: UPDATE_ANUNCIO,
                    variables: { ...this.me.anuncios[0], tags: this.tagsIds },
                })
                .then(() => {
                    this.$router.replace({ name: "user-anuncios" });
                })
                .catch((errors) => {
                    this.erros = errors.graphQLErrors[0].extensions.validation;
                });
        },
    },
};
</script>