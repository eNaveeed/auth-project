<template>
  <div class="w-full h-full bg-[#0F0F0F] relative ">
    <BackgroundCircles />
    <div
      class="w-full gap-10 mx-auto top-1/2 left-1/2-translate-x-1/2 -translate-y-1/2 absolute z-10 flex justify-between py-5 px-40"
    >
    
    <!-- <Header/> -->
      <div class="flex justify-between">
        <div class="flex justify-center items-center flex-col">
        <h1 class="text-[96px] font-semibold">Welcome back.!</h1>
        <span class="text-purple-500">.</span>
        <p class="mt-4 text-lg text-white">
          <a href="#" class="underline hover:text-purple-500">
            Skip the lag?
          </a>
        </p>
      </div>
      </div>
      </div>
      <div
        class="md:w-1/2 border border-white/50 bg-[linear-gradient(90deg,rgba(191,191,191,0.31),rgba(0,0,0,0))] rounded-[20px] px-10 pt-16 pb-12"
      >
        <div class="space-y-3 mb-3">
          <h1 class="text-white font-bold text-2xl">Login</h1>
          <p class="">Glad you're back.!</p>
        </div>
        <form class="space-y-4 w-full" @submit.prevent="handleLogin">
          <!-- Username field -->
          <input
            type="text"
            v-model="username"
            placeholder="Username"
            class="block w-full px-4 py-1.5 outline-none focus:outline-none bg-transparent border border-white rounded-full text-white"
            name="username"
          />

          <!-- Password field -->
          <input
            type="password"
            v-model="password"
            placeholder="Password"
            class="block w-full px-4 py-1.5 text-white outline-none focus:outline-none bg-transparent border border-white rounded-full"
            name="password"
          />

          <!-- Remember me checkbox -->
          <div class="flex items-center">
            <input type="checkbox" id="remember-me" class="mr-2" />
            <label for="remember-me" class="text-gray-400"
              >Remember me</label
            >
          </div>
          <!-- Login button -->
          <button
            type="submit"
            class="w-full py-2 text-white bg-gradient-to-r from-purple-500 to-indigo-600 rounded-lg"
          >
            Login
          </button>
          <!-- Forgot password link -->
          <a
            href="#"
            class="block text-center text-white mt-3 text-[16px] font-medium"
            >Forgot password?</a
          >
        </form>
        <div class="bg-white w-full h-px mt-[58px] mb-6"></div>
        <div class="flex gap-x-4 justify-center">
          <img src="../../assets/google.svg" width="42" height="42" alt="" />
          <img src="../../assets/githup.svg" width="42" height="42" alt="" />
          <img src="../../assets/facebook.svg" width="42" height="42" alt="" />
        </div>

        <!-- Footer links -->
        <div class="mt-[50px] text-white space-y-2">
          <p class="inline-block font-medium">Don't have an account? 
             <NuxtLink to="/signup">
              signup
                     </NuxtLink>
                     

          </p>
          <div class="flex gap-x-2">
            <a href="#" class="inline-block shrink-0 overflow-hidden ml-auto">Terms &#38; Conditions</a>
            <a href="#" class="inline-block shrink-0 overflow-hidden">Support</a>
            <a href="#" class="inline-block shrink-0 overflow-hidden">Customer Care</a>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
import BackgroundCircles from "@/components/login/BackgroundCircles.vue";
import axios from "axios";
import { useToast } from 'vue-toastification';



export default {
  data(){
    return{
      username:"",
      password:""
    }
  },
  components: {
    BackgroundCircles,
  }, 
  methods: {
async handleLogin(event) {
  event.preventDefault();
   const toast = useToast();

  if(!this.username || !this.password) return // gaurd clauses / early returns
  try {
    const response = await axios.get("http://localhost:3001/users", {
      params: {
        username: this.username,
        password: this.password
      }
    });

    const data = response.data

    console.log("******************** _____________________ ",data)

    if(data.length === 0 || !data[0].username || !data[0].password){
        toast.error('No user found with these credentials.', {
            position: "top-right",
            timeout: 3000,
          });
    } else {
      toast.success("You\'re successfully logged in", {
          position: "top-right",
          timeout: 3000,
        });

               this.$router.push("/dashboard");

    }


  } catch (error) {
    console.error("Error during login:", error);
  }
}

  }
};
</script>

<style >
</style> 

