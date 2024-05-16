<!-- <template>
  <div> 
    <input type="text" placeholder="Ingrese su nombre" id="" v-model="nombre" /><br><br>
    <input type="text" name="" id="" placeholder="Ingrese su apellido" v-model="apellido" /><br><br>
    <input type="email" name="" id="" placeholder="Ingrese su email" v-model="correo" /> <br><br>
    <input type="date" name="" id="" v-model="fechana" /><br><br>

    <button @click="Guardar()"> Enviar</button>
    <table>
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Apellido</th>
          <th>Correo</th>
          <th>Fecha_nacimiento</th>
          <th>Edad</th>
          <th>Opciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item,i) in data" :key="i">
        <td>{{item.nombre}}</td>
        <td>{{item.apellido}}</td>
        <td>{{item.correo}}</td>
        <td>{{item.fecha_nacimiento}}</td>
        <td>{{ calcularedad(item.fecha_nacimiento) }}</td>
        <td><button @click="editar(i)">📝</button></td>
        <td><button @click="eliminar(i)">❌</button></td>   
      </tr>
    </tbody>
    </table>
  </div>
</template>

<script setup>
import {ref} from "vue"

let nombre= ref("")
let apellido= ref("")
let correo= ref("")
let fechana= ref("")
let ed=true
// let index=ref(null)


let data=ref([])

function Guardar(i) {


  if(ed === true){
     let inf = {
    nombre: nombre.value,
    apellido: apellido.value,
    correo: correo.value,
    fecha_nacimiento: fechana.value,
  };


  data.value.push(inf);  
 
  }else{
       data.value[i].nombre = nombre.value;
       data.value[i].apellido = apellido.value;
       data.value[i].correo = correo.value;
       data.value[i].fecha_nacimiento= fecha_nacimiento.value;
       data.value[i].edad = edad.value;
       ed=false
   
      // index.value=null
  }

}

function calcularedad(fechana) {
  let fecha_nacimiento = new Date(fechana);
  let fecha_actual = new Date();
  let edad = fecha_actual.getFullYear() - fecha_nacimiento.getFullYear();
  return edad;
}

function eliminar(i){
data.value.splice(i, 1)
}
function editar(i){

  data.value[i].editable = true; // Activar el modo edición
  nombre.value = data.value[i].nombre
apellido.value = data.value[i].apellido
correo.value = data.value[i].correo
  fecha_nacimiento.value = data.value[i].fecha_nacimiento
  edad.value = data.value[i].edad

  ed=false

    
}

</script>

<style >
</style> 
 -->
 <template >
 <div id="contenedorInicial" style="background-image: url('img/fondof.jpg');">
  <div id="contenedor" >
    
    <div id="formularioTabla">


        <div id="tabla">
          <table>
            <thead>
              <tr>
                <th>Nombre</th>
                <th>Precio</th>
                <th>Costo</th>
                <th>Cantidad</th>
                <th>Proveedor</th>
                <th>Aumentar</th>
                <th>Disminuir</th>
                <th>Ganacias</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(item, i) in data" :key="i">
                <th>{{ item.nombre }}</th>
                <th>{{ item.precio }}</th>
                <th>{{ item.costo }}</th>
                <th>{{ item.cantidad }}</th>
                <th>{{ item.proveedor }}</th>
                <th><button id="botonesad" @click="aumentar(i)">+</button></th>
                <th><button id="botonesad" @click="disminuir(i)">-</button></th>
                <th>{{ item.ganancia }}</th>
              
              </tr>
            </tbody>  
          </table>
        </div>
      </div>

      <hr>
    
      <div id="botones">
      <!-- totales en general -->
<!-- Button trigger modal -->
<button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModalScrollable">
Totales
</button>

<!-- Modal -->
<div class="modal fade" id="exampleModalScrollable" data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1" aria-labelledby="exampleModalScrollableLabel" aria-hidden="true">
  <div class="modal-dialog modal-dialog-scrollable modal-dialog-centered">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        <div id="totales">
      <h2>Costo Total:<span style="color: green;">{{ costo_total() }}</span></h2>
      <h2>Precio Total:<span style="color: green;">{{ PrecioTotal() }}</span></h2>
      <h2>Ganacia Total:<span style="color: green;">{{ ganaciasTotal() }}</span></h2>
      </div>
      </div>
    </div>
  </div>
</div>
    <!-- formulario de inventario -->
      <!-- Button trigger modal -->
<button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleModal">
 Agregar inventario
</button>

<!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog modal-dialog-scrollable modal-dialog-centered">
    <div class="modal-content">
      <div class="modal-header">
        <h1 class="modal-title fs-5" id="exampleModalLabel">Formulario</h1>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        <!-- <div id="Alertas">
        <p v-if="alerta5" class="error">El campo ganancias dene ser mayor a 0 </p>

    </div> -->
    <svg xmlns="http://www.w3.org/2000/svg" class="d-none">
            <symbol id="exclamation-triangle-fill" viewBox="0 0 16 16">
              <path d="M8.982 1.566a1.13 1.13 0 0 0-1.96 0L.165 13.233c-.457.778.091 1.767.98 1.767h13.713c.889 0 1.438-.99.98-1.767L8.982 1.566zM8 5c.535 0 .954.462.9.995l-.35 3.507a.552.552 0 0 1-1.1 0L7.1 5.995A.905.905 0 0 1 8 5zm.002 6a1 1 0 1 1 0 2 1 1 0 0 1 0-2z"/>
            </symbol>
           </svg>

      <div class="alert alert-danger d-flex align-items-center" role="alert" v-if="alerta5"  >
        <svg class="bi flex-shrink-0 me-2" role="img" aria-label="Danger:"><use xlink:href="#exclamation-triangle-fill"/>
        </svg>
           <div>
          El campo ganancias debe ser mayor a 0
           </div>
     </div>

    <div class="datos">

      <svg xmlns="http://www.w3.org/2000/svg" class="d-none">
        <symbol id="check-circle-fill" viewBox="0 0 16 16">
           <path d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zm-3.97-3.03a.75.75 0 0 0-1.08.022L7.477 9.417 5.384 7.323a.75.75 0 0 0-1.06 1.06L6.97 11.03a.75.75 0 0 0 1.079-.02l3.992-4.99a.75.75 0 0 0-.01-1.05z"/>
        </symbol>
      </svg>

<div class="alert alert-success d-flex align-items-center" role="alert" v-if="alertafinal">
  <svg class="bi flex-shrink-0 me-2" role="img" aria-label="Success:"><use xlink:href="#check-circle-fill"/></svg>
  <div>
    Los datos fueron guargados correctamente
  </div>
</div>
      <label for="nomp">Nombre del producto: </label>
        <input type="text" placeholder="ingrese el nombre" id="caja" v-model="nombre" />
          <svg xmlns="http://www.w3.org/2000/svg" class="d-none">
            <symbol id="exclamation-triangle-fill" viewBox="0 0 16 16">
              <path d="M8.982 1.566a1.13 1.13 0 0 0-1.96 0L.165 13.233c-.457.778.091 1.767.98 1.767h13.713c.889 0 1.438-.99.98-1.767L8.982 1.566zM8 5c.535 0 .954.462.9.995l-.35 3.507a.552.552 0 0 1-1.1 0L7.1 5.995A.905.905 0 0 1 8 5zm.002 6a1 1 0 1 1 0 2 1 1 0 0 1 0-2z"/>
            </symbol>
           </svg>

      <div class="alert alert-danger d-flex align-items-center" role="alert" v-if="alerta"  >
        <svg class="bi flex-shrink-0 me-2" role="img" aria-label="Danger:"><use xlink:href="#exclamation-triangle-fill"/>
        </svg>
           <div>
           El campo nombre esta vacio
           </div>
     </div>
   </div>
       
        <!-- <p v-if="alerta" class="error" >El campo nombre esta vacio</p> -->
   <div class="datos">
     <label for="precio">Precio: </label>
       <input type="number" placeholder="ingrese el precio" id="caja"  v-model="precio"/>
         <svg xmlns="http://www.w3.org/2000/svg" class="d-none">
           <symbol id="exclamation-triangle-fill" viewBox="0 0 16 16">
             <path d="M8.982 1.566a1.13 1.13 0 0 0-1.96 0L.165 13.233c-.457.778.091 1.767.98 1.767h13.713c.889 0 1.438-.99.98-1.767L8.982 1.566zM8 5c.535 0 .954.462.9.995l-.35 3.507a.552.552 0 0 1-1.1 0L7.1 5.995A.905.905 0 0 1 8 5zm.002 6a1 1 0 1 1 0 2 1 1 0 0 1 0-2z"/>
           </symbol>
         </svg>

       <div class="alert alert-danger d-flex align-items-center" role="alert" v-if="alerta1"  >
         <svg class="bi flex-shrink-0 me-2" role="img" aria-label="Danger:"><use xlink:href="#exclamation-triangle-fill"/></svg>
            <div>
               El campo precio debe ser mayor a 0
            </div>
       </div>
  </div>

        <div class="datos">
          <label for="costo">Costo: </label>
             <input type="number" placeholder="ingrese el costo" id="caja" v-model="costo" />
                <svg xmlns="http://www.w3.org/2000/svg" class="d-none">
                  <symbol id="exclamation-triangle-fill" viewBox="0 0 16 16">
                    <path d="M8.982 1.566a1.13 1.13 0 0 0-1.96 0L.165 13.233c-.457.778.091 1.767.98 1.767h13.713c.889 0 1.438-.99.98-1.767L8.982 1.566zM8 5c.535 0 .954.462.9.995l-.35 3.507a.552.552 0 0 1-1.1 0L7.1 5.995A.905.905 0 0 1 8 5zm.002 6a1 1 0 1 1 0 2 1 1 0 0 1 0-2z"/>
                  </symbol>
                </svg>

           <div class="alert alert-danger d-flex align-items-center" role="alert" v-if="alerta2"  >
             <svg class="bi flex-shrink-0 me-2" role="img" aria-label="Danger:"><use xlink:href="#exclamation-triangle-fill"/></svg>
                <div>
                  El campo costo debe ser mayor a 0
                </div>
           </div>
        </div>

        <div class="datos">
          <label for="cantidad">Cantidad: </label>
             <input type="number" placeholder="ingrese el costo" id="caja" v-model="cantidad" />
               <svg xmlns="http://www.w3.org/2000/svg" class="d-none">
                  <symbol id="exclamation-triangle-fill" viewBox="0 0 16 16">
                    <path d="M8.982 1.566a1.13 1.13 0 0 0-1.96 0L.165 13.233c-.457.778.091 1.767.98 1.767h13.713c.889 0 1.438-.99.98-1.767L8.982 1.566zM8 5c.535 0 .954.462.9.995l-.35 3.507a.552.552 0 0 1-1.1 0L7.1 5.995A.905.905 0 0 1 8 5zm.002 6a1 1 0 1 1 0 2 1 1 0 0 1 0-2z"/>
                  </symbol>
               </svg>

        <div class="alert alert-danger d-flex align-items-center" role="alert" v-if="alerta3"  >
          <svg class="bi flex-shrink-0 me-2" role="img" aria-label="Danger:"><use xlink:href="#exclamation-triangle-fill"/></svg>
            <div>
               El campo cantidad debe ser mayor a 0
            </div>
        </div>
    </div>

        <div class="datos">
          <label for="nompro">Nombre del proveedor: </label>
             <input type="text" placeholder="ingrese el nombre del proveedor"  id="caja" v-model="proveedor"/>
               <svg xmlns="http://www.w3.org/2000/svg" class="d-none">
                 <symbol id="exclamation-triangle-fill" viewBox="0 0 16 16">
                   <path d="M8.982 1.566a1.13 1.13 0 0 0-1.96 0L.165 13.233c-.457.778.091 1.767.98 1.767h13.713c.889 0 1.438-.99.98-1.767L8.982 1.566zM8 5c.535 0 .954.462.9.995l-.35 3.507a.552.552 0 0 1-1.1 0L7.1 5.995A.905.905 0 0 1 8 5zm.002 6a1 1 0 1 1 0 2 1 1 0 0 1 0-2z"/>
                 </symbol>
               </svg>
         <div class="alert alert-danger d-flex align-items-center" role="alert" v-if="alerta4"  >
           <svg class="bi flex-shrink-0 me-2" role="img" aria-label="Danger:"><use xlink:href="#exclamation-triangle-fill"/></svg>
             <div>
               El campo proveedor esta vacio
            </div>
        </div>
     </div>
        <!-- <button id="boton" @click="agregar()">Agregar</button> -->
 </div>
       <div class="modal-footer">
           <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cerrar</button>
             <button type="button" class="btn btn-primary" @click="agregar()">Agregar</button>
      </div>
     </div>
  </div>
</div>
</div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
let nombre = ref("");
let precio = ref("");
let costo = ref("");
let cantidad = ref("");
let proveedor = ref("");
let alerta = ref(false);
let alerta1 = ref(false);
let alerta2 = ref(false);
let alerta3 = ref(false);
let alerta4 = ref(false);
let alerta5 = ref(false);
let alertafinal= ref(false)
let costoTotal = ref(0);
let precioTotal = ref(0);
let GananciaTotal=ref(0);
let data = ref([]);

function agregar() {
  
  if (alert()) {
return;
   };
   if( agregar){
    alertafinal.value = true
    setTimeout(()=>{
      alertafinal.value= false

    },4000)
    }
   
    // let ganancia=(precio.value - costo.value) * cantidad.value;
    let ganancia =(precio.value * cantidad.value)- (costo.value * cantidad.value)
    
   
  //   if ( ganancia <= 0) {
  //   console.log(ganancia)
  //   alerta5.value = true;
  //   setTimeout(() => {
  //     alerta5.value = false;
  //   }, 3000);
  //   return true;
  // }
    
    let informacion = {
      nombre: nombre.value,
      precio: precio.value,
      costo: costo.value,
      cantidad: cantidad.value,
      proveedor: proveedor.value,
      ganancia:ganancia
    }
  
    data.value.push(informacion);
    limpiar();
  }

  function validarGanancia() {
  // let ganancia = (precio.value - costo.value) * cantidad.value;
  let ganancia =(precio.value * cantidad.value)- (costo.value * cantidad.value)
  return ganancia <= 0;
}

// function ganacias(item) {
//   ganancia = (item.precio - item.costo) * item.cantidad;

// return ganancia;
// }

// function ganacias(item,i) {
//   let ganancia = (item.precio - item.costo) * item.cantidad;
//   return ganancia;
// }

function alert() {
  if (!nombre.value) {
    alerta.value = true; //nos muestra el mensaje

    setTimeout(() => {
      alerta.value = false; // nos oculta el mensaje
    }, 3000);
    return true; //retorna la informacio
  } else if (precio.value <= 0) {
    alerta1.value = true;
    setTimeout(() => {
      alerta1.value = false;
    }, 3000);
    return true;
  } else if (costo.value <= 0) {
    alerta2.value = true;
    setTimeout(() => {
      alerta2.value = false;
    }, 3000);
    return true;
  } else if (cantidad.value <= 0) {
    alerta3.value = true;
    setTimeout(() => {
      alerta3.value = false;
    }, 3000);
    return true;
  }else if(proveedor.value <= 0){
    alerta4.value = true;
    setTimeout(() => {
      alerta4.value = false;
    }, 3000);
    return true;
  

  }
  if ( validarGanancia()) {
    alerta5.value = true;
    setTimeout(() => {
      alerta5.value = false;
    }, 3000);
    return true;
  }
  return false; // retorna la informacion y la oculta
}


function limpiar(){
  nombre.value=""
  precio.value=""
  costo.value=""
  cantidad.value=""
  proveedor.value=""
}
function recalcularGanancias(i) {
let item = data.value[i];
item.ganancia = (item.precio * item.cantidad ) - (item.costo * item.cantidad)
}

function aumentar(i) {
  data.value[i].cantidad++;
  recalcularGanancias(i)

}

function disminuir(i) {
  data.value[i].cantidad--;
  recalcularGanancias(i)
}

function costo_total() {
  costoTotal = 0;
  for (let item of data.value) {
    costoTotal += item.costo ;
  }
  return costoTotal;
}

// Precio total del inventario: multiplicar precio por precio y sumar todos los productos
function PrecioTotal() {
  precioTotal = 0;
  for (let item of data.value) {
    precioTotal += item.precio;
  }
  return precioTotal;
}
// Ganancia total: resta entre precio total menos costo total
function ganaciasTotal() {
GananciaTotal=0;
for (let item of data.value) {
    GananciaTotal += item.ganancia;
  }
  return GananciaTotal;
}


</script>
<style>

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

template{
  width:100%;
  background-size: cover;
}
#contenedor {
  width:100%;
  height:auto;
  background-size: cover;
  padding-top:5%;
  background-color:rgba(255, 255, 255, 0.7);
  height:100vh;
}
#totales{
  font-size: 15px;
}
#caja{
  width: 100%;
height: 6vh;
}
.datos label{
  /* font-size:23px; */
  font-weight:700;

}
.datos{
margin-top:4%;
/* button */
}

#tabla{
display:grid;
justify-content:center;
text-align:center;
text-align:item;

width:100%;
}
table{
border: 1px solid black;
border-collapse: collapse;
width: 100%;

}
thead th {
  border: 1px solid black;
  width: 100%;
  background-color: black;
  color:white;
  width: 100%;
  padding: 1vh;
  text-align: center;
  font-size: 23px;
  font-family: cursive;
}
tbody th {
 border: 1px solid black;
 width: 100%;
  padding: 1vh;
  text-align: center;

    
}
tbody{
  background-color:white;
}
tbody tr:nth-child(even) {
  background-color: #f2f2f2; /* Color de fondo para las filas impares */   
}
#totales h1{
  /* font-size:20px; */
  font-family: cursive;
  font-weight:bolder;
}
#botonesad{
  /* padding: 1%; */
 width: 40%; 
  border:0px;
  background-color:#33cf67;
  font-size: 20px;
  font-weight :1000;

}
#botones{
   display:flex;
   gap:20px;
   justify-content:center;
}

.bi{
  width:10% ;
  height:4vh;
}


.alert {
  margin-top: 1%;
  padding: 1%;
  z-index:1;
  display: flex;
  align-items: center; /* Centra verticalmente los elementos */
  justify-content: center; /* Centra horizontalmente los elementos */
}
.btn{
 font-weight:700;
 font-size:20px;
}
#contenedorInicial{
  width:100%;
  height:100vh;
  
}



</style>