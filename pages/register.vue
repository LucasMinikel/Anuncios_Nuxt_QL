<template>
    <div class="mt-10 flex justify-center">
        <form action="" class="w-6/12" @submit.prevent="submit">
            <h2 class="mb-4 text-2xl font-bold">Criar conta</h2>
            {{ form }}
            <div class="mb-4">
                <label for="email" class="inline-block mb-1 font-medium"
                    >Email</label
                >
                <input
                    type="email"
                    name="email"
                    id="email"
                    class="
                        bg-gray-200
                        border-2 border-gray-200
                        rounded-lg
                        w-full
                        h-10
                        px-4
                    "
                    placeholder="seuemail@email.com"
                    v-model="form.email"
                />
            </div>
            <div class="mb-4">
                <label for="name" class="inline-block mb-1 font-medium"
                    >Nome</label
                >
                <input
                    type="name"
                    name="name"
                    id="name"
                    class="
                        bg-gray-200
                        border-2 border-gray-200
                        rounded-lg
                        w-full
                        h-10
                        px-4
                    "
                    placeholder="Meu nome"
                    v-model="form.name"
                />
            </div>
            <div class="mb-4">
                <label for="password" class="inline-block mb-1 font-medium"
                    >Senha</label
                >
                <input
                    type="password"
                    name="password"
                    id="password"
                    class="
                        bg-gray-200
                        border-2 border-gray-200
                        rounded-lg
                        w-full
                        h-10
                        px-4
                    "
                    placeholder="minhasenha123!"
                    v-model="form.password"
                />
            </div>
            <button
                type="submit"
                class="p-4 bg-blue-500 text-white font-medium rounded-lg"
            >
                Criar
            </button>
        </form>
    </div>
</template>
<script>
import CREATE_USER from "@/graphql/CreateUser.gql";
export default {
    data() {
        return {
            form: {
                email: "",
                name: "",
                password: "",
            },
        };
    },
    methods: {
        createUser() {
            this.$apollo
                .mutate({
                    mutation: CREATE_USER,
                    variables: this.form,
                })
                .then(() => {
                    this.$axios
                        .$get("/sanctum/csrf-cookie")
                        .then((res) => {
                            try {
                                this.$auth.loginWith("laravelSanctum", {
                                    data: this.form,
                                });
                            } catch (error) {}
                        })
                        .then(() => {
                            this.$router.replace({ name: "index" });
                        });
                });
        },
        submit() {
            this.createUser();
        },
    },
};
</script>
