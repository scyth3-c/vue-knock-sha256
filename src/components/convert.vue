<template>

 <b-container class="position-relative">
    
    <b-card class="bg-dark mt-3 shadow rounded">
        
        <span><b-badge variant="primary" class="p-2 w-100"> <b-icon icon="lock-fill"></b-icon> convertir </b-badge></span>
        
        <b-card class="mt-3 bg-dark shadow rounded">
 
             <input type="text" class="form-control" v-model="texto" placeholder="texto">
              <span><b-badge class="mt-2 w-100" variant="dark">resultado <b-icon icon="arrow-bar-down"></b-icon></b-badge></span>
             <div class="w-70 bg-secondary rounded mt-3 text-align" style="height: 300px;" >
              
              <div class="p-2">
                   <span  v-if="auto == 'false'" class="font-weight-bold text-white" style="word-wrap: break-word;"> 
                    {{hash}}
                </span>
                   <span  v-else class="font-weight-bold text-white" style="word-wrap: break-word;"> 
                    {{autohash}}
                </span>
              </div>
               
             </div>
            <b-button :disabled="auto == 'true'" class="mt-3 w-100" @click="convertHash">convertir</b-button>
              <div><b-badge :class="hex_class" @click="hex">hex</b-badge> <b-badge :class="base64_class" @click="base64">base64</b-badge> 
              <b-form-checkbox id="checkbox-1" v-model="auto" value="true" unchecked-value="false" class="float-right text-white font-weight-bold my-2">auto convert</b-form-checkbox>
              
              </div>

     
        </b-card>
 
    </b-card>

 </b-container>


</template> 


<style scoped>
 
 .hex-active {
     background-color: lightseagreen;
     color: whitesmoke;
     cursor: pointer;
 }
 .hex-desactive {
     background-color: lightgrey;
     color: darkslategray;
     cursor: pointer;
 }

 .base64-active {
     background-color: lightseagreen;
     color: whitesmoke;
     cursor: pointer;
 }
 .base64-desactive{
     background-color:lightgrey;
     color: darkslategray;
     cursor: pointer;
 }
input   {
    font-weight: bold;
}
</style>


<script>
export default {
    name: 'convert',
    data() {
        return {
           
           texto: 'prueba',
           hash: 'esta noche',
           bgbool: true,
           bg: 'hex',
           auto: 'false',

        }
    },
    methods: {
          convertHash() {
            this.hash = '';
            this.hash = this.GLOBAL.shade(this.texto,this.bg);
            this.share();
         },
         hex(){
            this.bgbool = true;
            this.bg = 'hex';
         },
         base64(){
             this.bgbool = false;
             this.bg = 'base64';
         },
         share() {
             this.$root.$emit('share_hash',this.hash);
         }
    },
    created() {
       this.convertHash();
      },
    computed: {
        hex_class() {
            const active = 'hex-active';
            const desactive = 'hex-desactive';
            return this.bgbool ? active : desactive;
        },
        base64_class(){
            const active = 'base64-active';
            const desactive = 'base64-desactive';
            return !this.bgbool ? active : desactive;
        },
        autohash(){
            this.convertHash();
            return this.hash;
        }
    }
}
</script>
