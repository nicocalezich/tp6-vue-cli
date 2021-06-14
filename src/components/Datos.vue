<template>

  <section class="src-components-datos"> 

    <table class="table" v-if="hayDatos()">
      <thead>
        <tr class="table-primary">
          <th class="table-primary" scope="col">Nombre</th>
          <th class="table-primary" scope="col">Edad</th>
          <th class="table-primary" scope="col">Mail</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(object,index) in data" :key="index" class="table-darprimaryk">
          <td class="table-primary">{{object.nombre}}</td>
          <td class="table-primary">{{object.edad}}</td>
          <td class="table-primary">{{object.email}}</td>
        </tr>
      </tbody>
    </table>

    <div class="alert alert-warning" role="alert" v-else>
      No se encontraron datos
    </div>
    
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-components-datos',
    props: [],
    mounted () {
      this.getDataAsync()
    },
    data () {
      return {
        url: 'https://60aa960a66f1d00017773022.mockapi.io/Usuarios',
        data: []
      }
    },
    methods: {

      //get con then catch
       getData(){
        this.axios(this.url)
        .then(response =>{
          this.data = response.data
        })
        .catch(error => console.error(error))
      },

      //get con async await
       async getDataAsync() {
        try {
          let respuesta = await this.axios(this.url)
          this.data = respuesta.data
        }
        catch(error) {
          console.error(error)
        }
      },

      hayDatos(){
        return this.data.length > 0
      }
    },


    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-datos {
    padding: 30px;
  }
</style>
