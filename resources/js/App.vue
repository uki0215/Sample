<template>
   <div>
       <navbar :app="this"></navbar>
       <spinner v-if="loading"></spinner>
       <div v-else-if="initiated">
            <router-view />
       </div>
       
   </div>
</template>

<script>
import navbar from './components/navbar';
    export default {
        name: 'app',
        components: {
            navbar
        },
        data() {
            return{
                user:null,
                loading:false,
                initiated:false,
                req:axios.create({
                    baseUrl:BASE_URL
                })
            };
        },
        mounted(){
            this.init();
        },
        methods: {

            init(){
                this.loading=true;
                
                this.req.get('auth/init').then(response=>{
                    this.user = response.data.user;
                    this.loading=false;
                    this.initiated=true;
                })
            }

        }
    };
</script>

<style>

</style>
