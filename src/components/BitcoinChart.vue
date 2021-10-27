<template>
    <v-container>
        <p>Aquí va a ir mi gráfica de bitcoin con {{cripto}} {{moneda}} {{plazo}}</p>
        <apexchart width="500" type="bar" :options="options" :series="series"></apexchart>

    </v-container>
</template>

<script>
export default {
    props: ['cripto','moneda','plazo'],

    watch:{
        cripto:function(newCripto,oldCripto){
            console.log(newCripto)
            console.log(oldCripto)
            this.cargarDatos();
        },
        moneda:function(newCripto,oldCripto){
            console.log(newCripto)
            console.log(oldCripto)
            this.cargarDatos();
        },
        plazo:function(newCripto,oldCripto){
            console.log(newCripto)
            console.log(oldCripto)
            this.cargarDatos();
        }
    },
    methods:{

        cargarDatos(){
            //TODO implementar aquí su llamada deberemos cambiar la data de categories y de data
            this.axios.get('').then((response)=>{
                console.log(response);
                this.options.xaxis;//Qué debemos meter aquí
                this.series.data;//Qué debemos meter aquí
            })
        }
    },

    data: ()=>({
      options: {
        chart: {
          id: 'vuechart-example'
        },
        xaxis: {
          categories: [1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998]
        }
      },
      series: [{
        name: 'series-1',
        data: [30, 40, 45, 50, 49, 60, 70, 91]
      }]
    })
}
</script>
