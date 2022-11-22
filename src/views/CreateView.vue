<script setup>
import { ref } from 'vue'
import axios from 'axios'
import { useRouter } from 'vue-router';
const title=ref('');
const image=ref('');
const router= useRouter()

const onFileChange = (e) =>{
    console.log(e.target.files[0]);
    image.value=e.target.files[0]
}

const submit= async ()=>{
    if(!title.value || !image.value){
        alert("por favor ingrese datos")
    }else{
        const formdata = new FormData();
        formdata.append('title',title.value);
        formdata.append('image',image.value);
         const res = await axios.post("http://localhost:8000/api/create", formdata);
         console.log(res)
        if(res.data.success){
            alert("Imagen subida exitosamente");
            title.value = "";
            image.value = "";
            router.push("/")
        }
    }
}
</script>

<template>
    <div>
        <div class="container my-5">
            <div class="row d-flex justify-content-center">
                <div class="col-xl-5 col-lg-5 col-md-8 col-sm-12">
                    <div class="my-3">
                        <router-link to="/"><button class="btn btn-secondary">Volver</button></router-link>                       
                    </div>
                    <div class="card">
                        <div class="card-header">
                            <h3>Crear Nuevo</h3>
                        </div>
                        <div class="card-body">
                            <form action="" @submit.prevent="submit">
                                <div class="my-2">
                                    <label for=""><b>Title</b></label>
                                    <input type="text" v-model="title" class="form-control">
                                </div>
                                <div class="my-2">
                                    <label for=""><b>Image</b></label>
                                    <input type="file" @change="onFileChange" class="form-control">
                                </div>
                                <button class="btn btn-primary" type="submit">Guardar</button>
                            </form>
                        </div>
                    </div>
                </div>
                
            </div>
        </div>
    </div>
  
</template>

<script>
export default {
    name: "CreateView",
}
</script>

<style>

</style>