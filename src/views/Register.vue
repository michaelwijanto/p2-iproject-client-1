<template>
  <div class="flex items-center justify-center py-44">
      <div class="max-w-2xl mx-auto">
	    <div class="bg-white bg-opacity-80 shadow-md border border-gray-200 rounded-lg max-w-sm py-10 px-20">
		  <form class="space-y-6 w-full flex flex-col justify-center items-center text-left" @submit.prevent="register">
			<h3 class="text-xl font-medium text-gray-900 dark:text-white">Register</h3>
			<div>
				<label for="email" class="text-sm font-medium text-gray-900 block mb-2 dark:text-gray-300">Email</label>
				<input type="email" class="bg-gray-50 border border-gray-300 text-gray-900 rounded-lg focus:border-blue-500 w-72 p-2.5" placeholder="name@company.com" v-model="user.email">
            </div>
            <div>
                <label for="password" class="text-sm font-medium text-gray-900 block mb-2 dark:text-gray-300">Password</label>
                <input type="password" class="bg-gray-50 border border-gray-300 text-gray-900 rounded-lg focus:border-blue-500 w-72 p-2.5" v-model="user.password">
            </div>
                <button type="submit" class="text-white bg-blue-700  hover:underline active:underline font-medium rounded-lg text-sm px-8 py-3 text-center">Register</button>
            <div class="text-sm font-medium text-gray-500 dark:text-gray-300">
                Already registered? <a href="#" class="text-blue-700 hover:underline" @click.prevent="toLogin">Login</a>
            </div>
            <p v-if="error" class="text-red-500 text-sm font-bold">{{errMsg}}</p>
		  </form>
	    </div>
      </div>
  </div>
</template>


<script>
export default {
    name: "Register",
    data() {
        return {
            user: {
                email: "",
                password: "",
            },
            errMsg: "",
            error: false,
        }
    },
    methods: {
        register() {
            this.$store.dispatch("register", this.user)
            .then(() => {
                return this.$store.dispatch("login", this.user)
            })
            .then(({data}) => {
                this.error = false;
                localStorage.setItem("access_token", data.access_token );
                this.$store.commit("set_is_logged_in", true);
                this.$router.push("/");
            })
            .catch((err) => {
                console.log(err.response.data.message);
                this.errMsg = err.response.data.message;
                this.error = true;
            })
        },
        toLogin() {
            this.$router.push("/Login");
        }
    }
}
</script>

<style>

</style>