<template>
  <div class="container border border-dark">
    <div class="row justify-content-center align-content-center">
        <div class="col-6 text-center pt-3">
            <form v-on:submit.prevent> 
                <div class="row justify-content-center">
                    <div class="col-4 mb-3">
                        <input v-model="num1" type="text" class="form-control rounded-pill" placeholder="Ingresa un numero">
                    </div>
                    <div class="col-2 mb-3">
                        <select v-model="operacion" class="form-select" >
                            <!--<option selected>Operacion</option>-->
                            <option value="1">+</option>
                            <option value="2">-</option>
                            <option value="3">*</option>
                            <option value="4">÷</option>
                        </select>
                    </div>
                    <div class="col-4 mb-3">
                        <input v-model.number="num2" type="text" class="form-control rounded-pill" placeholder="Ingresa un numero">
                    </div>
                </div>
            </form>
        </div>
    </div>
    <hr>
    <div class="row justify-content-center align-content-center">
        <div class="col-6 text-center">
            <h2>Resultado: <span :class="sum || rest || mult || divi">{{num1}} {{signo}} {{num2}} <span v-if="resultado">=</span> {{respuesta}}</span></h2>
            <div class="py-3">
                <button class="btn btn-primary" @click="guardar">Generar json</button>
            </div>
            <hr>
            <div class="row justify-content-center align-content-center">
                <div class="col">
                    <div v-show="mostrar2" class="bg-info py-1">
                    <!--<h4 v-for="(item, index) in recuperar" :key="item">{{index}} : {{item}}</h4>-->
                    <h4>{{value_json}}</h4>
                    <!--<h4>{{recuperar}}</h4>-->
                    </div>
                </div>
            </div>
            
            <div class="py-3">
                <button class="btn btn-danger" @click="borrar">Borrar</button>
            </div>
        </div>

    </div>
  </div>
</template>

<script>
//import {mapState, mapMutations} from 'vuex'

export default {
    data() {
        return {
            operacion: '',
            signo:'',
            respuesta:'',
            mostrar:false,
            mostrar2:false,
            num1:'',
            num2:'',
            otro:0,
            contenido:{
                "a":"",
                "b":"",
                "c":"",
                "operador":""
            },
            value_json:'',
            recupera:{}
        }
    },
    computed: {
        //...mapState(['valor1','valor2']),
        resultado(){
            if(this.respuesta !='' ){
                return this.mostrar=true
            }
        },
        sum(){
            if(this.operacion ==='1'){
                return this.respuesta= parseFloat(this.num1) + parseFloat(this.num2), this.signo = '+', this.corregir()
            }
        },
        rest(){
            if(this.operacion ==='2'){
                return this.respuesta=parseFloat(this.num1) - parseFloat(this.num2), this.signo = '-', this.corregir()
            }
        },
        mult(){
            if(this.operacion ==='3'){
                return this.respuesta=parseFloat(this.num1) * parseFloat(this.num2), this.signo = '*', this.corregir()
            }
        },
        divi(){
            if(this.operacion ==='4'){
                return this.respuesta=parseFloat(this.num1) / parseFloat(this.num2), this.signo = '÷', this.corregir()
            }
        },
        recuperar(){
            return this.recupera = JSON.parse(this.value_json)
        }
    },
    methods: {
        //...mapMutations(['suma']),
        guardar(){
            this.contenido.a=parseFloat(this.num1);
            this.contenido.b=parseFloat(this.num2);
            this.contenido.c=parseFloat(this.respuesta);
            this.contenido.operador=this.signo;
            this.value_json=JSON.stringify(this.contenido, null, '\n');
            this.mostrar2 = true;
            console.log(this.value_json);
        },
        borrar(){
            this.num1 = '',
            this.num2 = '',
            this.respuesta = '',
            this.signo = '',
            this.mostrar = false,
            this.mostrar2 = false,
            this.operacion = '',
            this.contenido.a='',
            this.contenido.b='',
            this.contenido.c='',
            this.contenido.operador=''
        },
        corregir(){
            if(isNaN(this.respuesta)){
                return this.respuesta = 0
            }else{
                return this.respuesta
            }
        }
        
    },
}
</script>

<style>
.vertical{
  writing-mode: vertical-rl;
  text-orientation: upright;
}

</style>