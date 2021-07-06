<template>
    <div>
        <Header/>

            <div class="container izquierda">

                <button class="btn btn-primary" v-on:click="nuevo()" >Nuevo instructor</button>
                <br><br>


                <table class="table table-hover">
                <thead>
                    <tr>
                        <th scope="col">Id</th>
                        <th scope="col">Nombre</th>
                        <th scope="col">Apellido Paterno</th>
                        <th scope="col">Apellido Materno</th>
                        <th scope="col">Sexo</th>
                        <th scope="col">RFC</th>
                        <th scope="col">Formación</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="instructor in sac" :key="instructor.ID_INSTRUCTOR" v-on:click="editar(instructor.ID_INSTRUCTOR)">
                        <th scope="row">{{ instructor.ID_INSTRUCTOR}}</th>
                        <td>{{ instructor.NOMBRE }}</td>
                        <td>{{ instructor.APELLIDO_PATERNO }}</td>
                        <td>{{ instructor.APELLIDO_MATERNO }}</td>
                        <td>{{ instructor.SEXO }}</td>
                        <td>{{ instructor.RFC }}</td>
                        <td>{{ instructor.FORMACION }}</td>
                    </tr>
            
                </tbody>
                </table>

            </div>

        <Footer />
    </div>
</template>
<script>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import axios from 'axios';
export default {
    name:"Dashboard",
    data(){
        return {
            sac:null,
            pagina:1
        }
    },
    components:{
        Header,
        Footer
    },
    methods:{
            editar(id){
                this.$router.push('/editar/' + id);
            },
            nuevo(){
                this.$router.push('/nuevo');
            }
    },
    mounted:function(){
        let direccion = "http://tabla-instructor.com/instructor?page=" + this.pagina;
        axios.get(direccion).then( data =>{
            this.sac = data.data;
        });
    }
}
</script>
<style  scoped>
    .izquierda{
        text-align: left;
    }
</style>