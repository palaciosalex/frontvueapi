<template>

<div class="row mt-3">
    <div class="col-md-6 offset-md-3">
        <div class="card">
            <div class="card-header bg-dark text-white text-center">Crear Producto</div>
            <div class="card-body">
                <form v-on:submit="guardar">
                    <div class="input-group mb-3">
                        <span class="input-group-text"><i class="fa-solid fa-gift"></i></span>
                        <input type="text" id="nombre" v-model="name" class="form-control"
                        maxlength="50" placeholder="Nombre" required />

                    </div>
                    <div class="input-group mb-3">
                        <span class="input-group-text"><i class="fa-solid fa-comment"></i></span>
                        <input type="number" id="stock" v-model="stock" class="form-control"
                         placeholder="stock" required />

                    </div>
                    <div class="input-group mb-3">
                        <span class="input-group-text"><i class="fa-solid fa-dollar-sign"></i></span>
                        <input type="number" id="precio" v-model="price" class="form-control"
                         placeholder="Precio" step="0.01" required />

                    </div>
                    <div class="d-grid col-6 mx-auto">
                        <button class="btn btn-success">
                            <i class="fa-solid fa-floppy-disk"></i> Guardar
                        </button>
                    </div>
                </form>
            </div>
        </div>

    </div>

</div>



</template>

<script>
    import { show_alerta, enviarSolicitud } from '../funciones';
    export default{
        data(){
            return{
                name: '',stock:'', price:'',url: 'http://localhost:80/api/product'
            }
        }
        ,methods:{
            guardar(){
                event.preventDefault();
                if(this.name.trim() === ''){
                    show_alerta('Escribe el nombre', 'warning', 'nombre');
                }
                else if(this.stock === ''){
                    show_alerta('Escribe la descripcion','warning','stock')
                }
                else if(this.price === ''){
                    show_alerta('Escribe el precio', 'warning', 'precio');
                }
                else{
                    var parametros = {name:this.name.trim(), stock: this.stock, price:this.price}
                    enviarSolicitud('POST',parametros,this.url,'Producto guardao');
                }
            }
        }
    }
</script>