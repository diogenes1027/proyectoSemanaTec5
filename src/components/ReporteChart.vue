<template>
    <v-container>
        <p>Candidad de alumnos que asistiría o no</p>
            <v-progress-circular
      indeterminate
      color="primary"
      v-if="loading"
    ></v-progress-circular>

        <apexchart v-if="!loading" width="100%" type="bar" :options="options" :series="series" v-bind:key="series[0].data"></apexchart>
    </v-container>
</template>

<script>
export default {
    props: ['contador'],

    watch:{
        series:function(newSeries,oldSeries){
            console.log(newSeries);
            console.log(oldSeries);
            
        },
        contador:function(){
            //console.log(newCripto)
            //console.log(oldCripto)
            this.cargarTrue();
            this.cargarFalse();
            
        }
        
    },

    mounted(){
        
      this.cargarTrue();
      this.cargarFalse();
    
    },

    methods:{
        async cargarTrue(){
            await this.axios.get('https://backendst5.herokuapp.com/si').then((response)=>{
                //console.log(response.data)
                this.si = response.data.length;
                console.log(this.si)
                this.series = [{
                    data: [this.si,this.no]
                }]
            })
        
        },
        async cargarFalse(){
            await this.axios.get('https://backendst5.herokuapp.com/no').then((response)=>{
                //console.log(response.data)
                this.no = response.data.length;
                console.log(this.no)
                this.series = [{
                    data: [this.si,this.no]
                }]
            })
        
        }
        
    },

    data: ()=>({
      si:0,
      no:0,
      loading:false,
      options: {
        xaxis: {
        categories: ["Sí asistiria", "No asistiría"],
        },
      },
      series: [{
        name: 'series-1',
        data: [30, 40]
      }]
    })
}
</script>