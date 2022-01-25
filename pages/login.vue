<template>
    <div class="mt-10 flex justify-center">
        <form action="" class="w-4/12" @submit.prevent="login">
            <h2 class="mb-4 text-2xl font-bold">Entrar</h2>
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
                <label for="email" class="inline-block mb-1 font-medium"
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
                Entrar
            </button>
        </form>
    </div>
</template>


<script>
export default {
    data() {
        return {
            form: {
                email: "",
                password: "",
            },
        };
    },
    methods: {
        login() {
            this.$axios.$get("/sanctum/csrf-cookie").then((res) => {
                try {
                    this.$auth.loginWith("laravelSanctum", {
                        data: this.form,
                    });
                } catch (error) {}
            });
        },
    },
};
</script>