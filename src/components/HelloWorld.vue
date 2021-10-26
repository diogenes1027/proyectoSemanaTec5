<template>
  <v-container>
    <h2>Hola {{usuario.nombre}} {{usuario.apellido}}, presionaste {{contador}} veces el botón</h2>
    <v-card style="padding:40px;">
    <v-text-field
      v-model="usuario.nombre"
      label="Dime tu nombre"
      hide-details="auto"
    ></v-text-field>
    <v-text-field
      v-model="usuario.apellido"
      label="Dime tu apellido"
      hide-details="auto"
    ></v-text-field>    
    <div style="margin-top:20px;">Contador {{contador}}</div>
    <v-btn  style="margin-top:20px;" elevation="2" @click="agregarAlContador" dark color="purple">Aumentar contador</v-btn>      
    </v-card>

  </v-container>
</template>

<script>

  export default {
    name: 'HelloWorld',

    mounted(){

    },

    methods:{
      agregarAlContador(){
        this.contador=this.contador+1;
      }
    },
    data: () => ({
      contador:0,
      usuario:{
        nombre:"",
        apellido:""
      }
    }),
  }
</script>
