<template>
    <div class="mt-10 flex justify-center">
        <form action="" class="w-6/12" @submit.prevent="submit">
            <h2 class="mb-4 text-2xl font-bold">Criar anúncio</h2>
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
                    v-model="form.anuncio_titulo"
                />
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
                    v-model="form.anuncio_local"
                />
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
                    v-model="form.anuncio_link"
                />
            </div>
            <div class="mb-4">
                <label for="tags" class="inline-block mb-1 font-medium"
                    >Tags</label
                >
                <v-select
                    inputId="tags"
                    :options="tags"
                    label="titulo"
                    :reduce="(tag) => tag.id"
                    multiple
                    v-model="form.tags"
                ></v-select>
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
                    v-model="form.anuncio_empresa"
                />
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
                    v-model="form.anuncio_logo"
                />
            </div>

            <div class="mb-4">
                <input
                    type="checkbox"
                    name="anuncio_marcado"
                    id="anuncio_marcado"
                    class="mr-2"
                    v-model="form.anuncio_marcado"
                /><label for="anuncio_marcado">Marcado</label>
            </div>
            <div class="mb-4">
                <input
                    type="checkbox"
                    name="anuncio_favorito"
                    id="anuncio_favorito"
                    class="mr-2"
                    v-model="form.anuncio_favorito"
                /><label for="anuncio_favorito">Favorito</label>
            </div>
            <button
                type="submit"
                class="p-4 bg-blue-500 text-white font-medium rounded-lg"
            >
                Entrar
            </button>
        </form>
    </div>
</template>

<script>
import ALL_TAGS from "@/graphql/AllTags.gql";
import CREATE_ANUNCIO from "@/graphql/CreateAnuncio.gql";
export default {
    data() {
        return {
            form: {
                anuncio_titulo: "",
                anuncio_local: "",
                anuncio_link: "",
                anuncio_empresa: "",
                anuncio_logo: "",
                anuncio_marcado: false,
                anuncio_favorito: false,
                tags: [],
            },
        };
    },
    apollo: {
        tags: {
            query: ALL_TAGS,
        },
    },
    methods: {
        createAnuncio() {
            this.$apollo
                .mutate({
                    mutation: CREATE_ANUNCIO,
                    variables: this.form,
                })
                .then(() => {
                    this.$router.replace({ name: "user-anuncios" });
                });
        },
        submit() {
            this.createAnuncio();
        },
    },
};
</script>
