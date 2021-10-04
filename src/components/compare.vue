<template>

<b-container class="position-relative">
   
   <b-card class="bg-dark mt-3 shadow rounded">
     <span><b-badge variant="success" class="w-100 p-2"> <b-icon variant="white" icon="check-circle-fill"></b-icon> compare</b-badge></span>
   
    <b-card  class="bg-dark rounded shadow mt-3">
     
     <span><b-badge class="bg-dark my-2">plain text <b-icon variant="white" icon="stickies"></b-icon> </b-badge></span>
     <input v-model="plain" type="text" class="form-control mb-3" placeholder="texto plano">

     <span><b-badge class="bg-dark my-2">sha256: <b-icon variant="white" icon="file-earmark-binary-fill"></b-icon> </b-badge></span>
     <input v-model="hash" type="text" class="form-control" placeholder="hash sha256">
    </b-card>
    <b-badge variant="dark mt-2" class="w-100">resultado <b-icon variant="white" icon="tv-fill"></b-icon> </b-badge>
    <b-card :class="conten_class" class="mt-3 rounded">
       <div :class="verify_class">
            <span v-if="auto == 'false'">{{estado}}</span> 
            <span v-else>{{autoverify}}</span>
            <br>
             <div style="font-size: 12px;">
            <span> [T {{bg}}]</span>      
            <span> [A {{auto}}]</span>
            <span> [L {{autolegacy}}]</span>
            </div>   
       </div>
    </b-card>
    
    <b-button :disabled="auto == 'true' " @click="verify" variant="secondary" class="w-100 mt-3">verificar</b-button>
    <b-form-checkbox id="checkbox-2" v-model="auto" value="true" unchecked-value="false" class="float-right text-white">auto verify</b-form-checkbox>
    <b-form-checkbox id="checkbox-3" v-model="legacy" value="true" unchecked-value="false" class="float-right text-white mr-2">legacy</b-form-checkbox>
    <div> <b-badge @click="hex" :class="hex_class">hex</b-badge> <b-badge @click="base64" :class="base64_class">base64</b-badge> </div>     
    
    

   </b-card>
   
  
    
</b-container>

    
</template>

<style scoped>
  
  .verify_active {
      background-color: #33FF96;
      color: darkslategrey;
       width: 100%;
      height: 130px;
      margin: 0;
      padding: 0;
      border-radius: 10px;
      text-align: center;
      font-family: monospace;
      font-weight: bold;
      font-size: 20px;
      line-height: 80px;
  }
  .verify_desactive {
      background-color:#FF7029;
      color: white;
      width: 100%;
      height: 130px;
      margin: 0;
      padding: 0;
      border-radius: 10px;
      text-align: center;
      font-family: monospace;
      font-weight: bold;
      font-size: 20px;
      line-height: 80px;
  }
   
   .conten-active {
       background-color: #33FF96;
   }
    .conten-desactive {
       background-color:#FF7029;
   }
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
 input {
     font-weight: bold;
 }

</style>



<script>
export default {
    name: 'compare',
    data() {
        return {
            plain: '',
            hash: '',
            estado: 'sin acciones',
            bg: 'hex',
            coinciden: false,
            bgbool: true,
            auto: 'false',
            legacy: 'false'
        }
    },
    methods: {
        verify() {
            if(this.plain != '' || this.hash != '') {
                const temphash = this.GLOBAL.shade(this.plain,this.bg);
                if(temphash == this.hash) {
                    this.coinciden = true;
                    this.estado = "COINCIDEN!";
                } else{
                    this.coinciden = false;
                    this.estado = "NO coinciden";
                }
            } else{
                this.estado = "datos vacios!"
            }
        },
        hex() {
            this.bgbool = true;
            this.bg = 'hex';
        },
        base64() {
           this.bgbool = false;
           this.bg = 'base64';
        }
    },
    computed: {
        verify_class() {
            const active = 'verify_active';
            const desactive = 'verify_desactive';
            return this.coinciden ? active : desactive;
        },
        conten_class() {
            const active = 'conten-active';
            const desactive = 'conten-desactive';
            return this.coinciden ? active : desactive;
        },
        hex_class() {
            const active = 'hex-active';
            const desactive = 'hex-desactive';
            return this.bgbool ? active : desactive;
        },
        base64_class() {
            const active = 'base64-active';
            const desactive = 'base64-desactive';
            return !this.bgbool ? active : desactive; 
        },
        autoverify() {
            this.verify();
            return this.estado;
        },
        autolegacy() {
            this.$root.$on('share_hash',(data)=>{
            this.hash = data || this.hash;
            });
             return this.legacy;
        }
    }

}
</script>