<template>
        <div>
          <Header />
            <div class="container">
                <form action="" class="form-horizontal">
                    <div class="form-group left">
                       <label for="" class="control-label col-sm-2">Nombre</label>
                       <div class="col-sm-10">
                          <input type="text" class="form-control" name="NOMBRE" id="NOMBRE" v-model="form.NOMBRE">
                       </div>
                    </div>
                    <div class="form-group left">
                       <label for="" class="control-label col-sm-2">Apellido Paterno</label>
                       <div class="col-sm-10">
                          <input type="text" class="form-control" name="APELLIDO_PATERNO" id="APELLIDO_PATERNO" v-model="form.APELLIDO_PATERNO">
                       </div>
                    </div>
                    <div class="form-group left row">
                      <div class="col">
                            <label for="" class="control-label col-sm-3">Apellido Materno</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="APELLIDO_MATERNO" id="APELLIDO_MATERNO" v-model="form.APELLIDO_MATERNO">
                            </div>
                        </div>
                        <div class="col">
                          <label for="" class="control-label col-sm-5">Sexo</label>
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
                              <label for="" class="control-label col-sm-2">Formación</label>
                              <div class="col-sm-7">
                                  <input type="text" class="form-control" name="FORMACION" id="FORMACION" v-model="form.FORMACION">
                              </div>
                        </div>
                    </div>


                    <div class="form-group">
                      <button type="button" class="btn btn-primary" v-on:click="editar()" >Editar</button>
                      <button type="button" class="btn btn-danger margen" v-on:click="eliminar()" >Eliminar</button>
                      <button type="button" class="btn btn-dark margen" v-on:click="salir()"  >Salir</button>
                    </div> 
                </form>
            </div>
          <!-- <Footer />   -->
        </div>
    
</template>
<script>
import Header from '@/components/Header.vue';
//import Footer from '@/components/Footer.vue';
import axios from 'axios';
export default {
  name:"Editar",
  components:{
    Header,
    //Footer
  },
  data:function(){
    return {
        form:{
          "ID_INSTRUCTOR":"",
          "NOMBRE" : "",
          "APELLIDO_PATERNO": "", 
          "APELLIDO_MATERNO" : "",
          "SEXO":"",
          "RFC" :"",
          "FORMACION" : "",
        }
    }
  },
  methods:{
      editar(){
          axios.put("http://tabla-instructor.com/instructor",this.form)
          .then( data =>{
              console.log(data);
          })
      },
      salir(){
        this.$router.push("/dashboard");
      },
      eliminar(){
        var enviar = {
            "ID_INSTRUCTOR" : this.form.ID_INSTRUCTOR,
        };
        axios.delete("http://tabla-instructor.com/instructor", { headers : enviar})
        .then( datos => {
            console.log(datos);
           this.$router.push("/dashboard");
        });

      }
  },
  mounted:function(){
      this.form.ID_INSTRUCTOR = this.$route.params.id;
      axios.get("http://tabla-instructor.com/instructorid="+ this.form.ID_INSTRUCTOR)
      .then( datos => {
        
        this.form.NOMBRE = datos.data[0].NOMBRE;
        this.form.APELLIDO_PATERNO = datos.data[0].APELLIDO_PATERNO;
        this.form.APELLIDO_MATERNO = datos.data[0].APELLIDO_MATERNO;
        this.form.SEXO = datos.data[0].SEXO;
        this.form.RFC = datos.data[0].RFC;
        this.form.FORMACION = datos.data[0].FORMACION;
        console.log(this.form);

      })
     
  }  
}
</script>
<style scoped>
 .left{
   text-align: left;
 };
 .margen{
   margin-left: 15px;
   margin-right: 15px;;
 }
</style>