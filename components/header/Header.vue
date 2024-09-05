<template>
  <header class="  w-full py-2.5">
    <nav class=" ">
        <ul class="flex      ">
            <li v-for='link in links' :key="link.id" class="shrink-0 ">
                <NuxtLink :to="link.path" class="text-nowrap font-semibold hover:bg-gray-900  py-2.5 px-10 rounded-full ">
                {{link.label}}
                </NuxtLink>
            </li>
        </ul>
    </nav>
  </header>
</template>

<script>
export default {
    data(){
        return{
            links: [{
                id:1,
               label: "Dashboard",
               path:"/dashboard"
            },{
                
                id:2,
                label: "Login",
                path:"/login"
            },
            {
                id:3,
                label: "Singup",
                path:"/signup"
                
            }]
        }
    }

}
</script>

<style>

</style>

