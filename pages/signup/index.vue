<template>
  <div class="w-full h-full bg-[#0F0F0F] relative">
    <BackgroundCircles />
    <div
      class="w-full gap-10 mx-auto top-1/2 left-1/2-translate-x-1/2 -translate-y-1/2 absolute z-10  py-10 px-40"
    >
    <Header  />
   <div class="flex justify-between">
       <div class="  flex flex-col justify-center items-center">
        <h1 class="text-[96px] font-semibold">Roll the Carpet.!</h1>
        <span class="text-blue-500">.</span>
        <p class="mt-4 text-lg text-white">
          <a href="#" class="underline hover:text-blue-500 focus:border-0 focus-visible:outline-0"> Skip the lag? </a>
        </p>
      </div>
      <div
      class="md:w-1/2 border border-white/20  rounded-[20px] px-10 py-15 drop-shadow-lg backdrop-blur-md"

      >
        <div class="space-y-3 mb-3">
          <h1 class="text-white font-bold text-2xl">Signup</h1>
          <p class="">Just some details to get you in!</p>
        </div>
        <form class="space-y-5 w-full">
          <!-- Username field -->
          <input
            type="text"
            v-model="username"
            placeholder="Username"
            class="block w-full px-4 py-1.5 outline-none focus:outline-none bg-transparent border border-white/20 rounded-full text-white"
          />
          <input
            type="Email/phone"
            v-model="email"
            placeholder="Email"
            class="block w-full px-4 py-1.5 outline-none focus:outline-none bg-transparent border border-white/20 rounded-full text-white"
          />

          <!-- Password field -->
          <input
            type="password"
            v-model="password"
            placeholder="Password"
            class="block w-full px-4 py-1.5 text-white outline-none focus:outline-none bg-transparent border border-white/20 rounded-full"
          />
                <input
                   type="password"
                  v-model="confirmPassword"
                 placeholder="Confirm Password"
                   class="block w-full px-4 py-1.5 text-white outline-none focus:outline-none bg-transparent border border-white/20 rounded-full"
                   />


          <!-- Signup button -->
          <button
            type="submit"
            class="w-full py-2 text-white bg-gradient-to-r from-[#111697] to-[#221EBF] rounded-lg gap-2"
            @click="signUpUser"
          >
            Signup
          </button>
        </form>
        <div class="bg-white/20 w-full h-px my-5"></div>
        <div class="flex gap-x-4 justify-center">
          <img src="../../assets/google.svg" width="42" height="42" alt="" />
          <img src="../../assets/githup.svg" width="42" height="42" alt="" />
          <img src="../../assets/facebook.svg" width="42" height="42" alt="" />
        </div>

        <!-- Footer links -->
        <div class="mt-[50px] text-white space-y-2">
          <p class="inline-block font-medium">Already Registered? 
              <NuxtLink to="/login">
              Login
                     </NuxtLink>
       </p>
          <div class="flex gap-x-2">
            <a href="#" class="inline-block shrink-0">Terms &#38; Conditions</a>
            <a href="#" class="inline-block shrink-0">Support</a>
            <a href="#" class="inline-block shrink-0 overflow-hidden">Customer Care</a>
          </div>
        </div>
      </div>
   </div>
    </div>
  </div>
</template>

<script>
import BackgroundCircles from "@/components/signup/BackgroundCircles.vue";
import Header from "@/components/header/Header.vue";
import axios from "axios";
import { useToast } from 'vue-toastification';
export default {
  name: "signup",
  components: {
    BackgroundCircles,Header
  },
  data() {
    return {
      username: "",
      password: "",
      email: "",
      confirmPassword: "",
    };
  },
  methods: {
    async signUpUser(e) {
      e.preventDefault();
      const toast = useToast();
      try {
        const userData = {
          username: this.username,
          email: this.email,
          password: this.password,
        };

       const response =  await axios.post("http://localhost:3002/users", userData);

       console.log('response __________________________ ',response)

       
              if (response.status === 201) {
          toast.success('Signup successful!', {
            position: "top-right",
            timeout: 3000,
             
            
          });

          this.$router.push("/login");
        } else {
          toast.error('Signup failed. Please try again.', {
            position: "top-right",
            timeout: 3000,
             
          });
        }


      } catch (error) {
        console.log("error", error);
        
         
          toast.error(`Signup failed. ${error.message}`, {
            position: "top-right",
             timeout: 3000,
           });
      }
    },
  },
};
</script>

<style></style>
