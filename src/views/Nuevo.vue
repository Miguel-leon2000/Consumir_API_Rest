<template>
    <div>
        <Header />
            <div class="container">
                

                <form action="" class="form-horizontal">
                    <div class="form-group left">
                       <label for="" class="control-label col-sm-2">NOMBRE</label>
                       <div class="col-sm-10">
                          <input type="text" class="form-control" name="NOMBRE" id="NOMBRE" v-model="form.NOMBRE">
                       </div>
                    </div>
                    <div class="form-group left">
                       <label for="" class="control-label col-sm-2">APELLIDO_PATERNO</label>
                       <div class="col-sm-10">
                          <input type="text" class="form-control" name="APELLIDO_PATERNO" id="APELLIDO_PATERNO" v-model="form.APELLIDO_PATERNO">
                       </div>
                    </div>
                    <div class="form-group left row">
                      <div class="col">
                            <label for="" class="control-label col-sm-3">APELLIDO_MATERNO</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="APELLIDO_MATERNO" id="APELLIDO_MATERNO" v-model="form.APELLIDO_MATERNO">
                            </div>
                        </div>
                        <div class="col">
                          <label for="" class="control-label col-sm-5">SEXO</label>
                          <div class="col-sm-7">
                              <input type="text" class="form-control" name="SEXO" id="SEXO" v-model="form.SEXO">
                          </div>
                        </div> 
                    </div>
                    <div class="form-group left row">
                         <div class="col">
                            <label for="" class="control-label col-sm-2">RFC</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="RFC" id="RFC" v-model="form.RFC">
                            </div>
                          </div>
                         <div class="col">
                              <label for="" class="control-label col-sm-2">FORMACION</label>
                              <div class="col-sm-7">
                                  <input type="text" class="form-control" name="FORMACION" id="FORMACION" v-model="form.FORMACION">
                              </div>
                        </div>
                    </div>


                    <div class="form-group">
                      <button type="button" class="btn btn-primary" v-on:click="guardar()" >Guardar</button>
                      <button type="button" class="btn btn-dark margen" v-on:click="salir()"  >Salir</button>
                    </div> 
                </form>


            </div>
        <!-- <Footer /> -->

    </div>
</template>
<script>
import Header from '@/components/Header.vue'
//import Footer from '@/components/Footer.vue'
import axios from 'axios';
export default {
    name:"Nuevo",
    data:function(){
        return {
            form:{
                "NOMBRE" : "",
                "APELLIDO_PATERNO": "", 
                "APELLIDO_MATERNO":"",
                "SEXO" :"",
                "RFC" : "",
                "FORMACION" : "",
                "token" : "" 
            }
        }
    },
    components:{
        Header,
        //Footer
    },
    methods:{
        guardar(){
            this.form.token = localStorage.getItem("token");
            axios.post("http://tabla-instructor.com/instructor",this.form)
            .then(data =>{
                console.log(data);
                this.makeToast("Hecho","Instructor creado","success");
                this.$router.push("/dashboard");
            }).catch( e =>{
                console.log(e);
                 this.makeToast("Error","Error al guardar","error");
            })
        },
        salir(){
            this.$router.push("/dashboard");
        },
        makeToast(titulo,texto,tipo) {
            this.toastCount++
            this.$bvToast.toast(texto, {
            title: titulo,
            variant: tipo,
            autoHideDelay: 5000,
            appendToast: true
            })
        }
        
    }
}
</script>
<style scoped>
.left{
    text-align:  left;
}
</style>