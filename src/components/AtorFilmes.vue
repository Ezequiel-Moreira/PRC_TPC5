<template>
  <v-container>
    <v-layout row wrap v-if="filmes.length > 0">
      <v-flex xs2>
        <h3>Filmes</h3>
      </v-flex>
      <v-flex xs10>
        <v-data-table
          :headers="headers"
          :items="filmes"
          class="elevation-1"
        >

            <template v-slot:no-data>
              <v-alert :value="true" color="error" icon="warming">
                Não foi possível apresentar a lista dos filmes.
              </v-alert>
            </template>

            <template v-slot:items="props">
              <tr @click="rowClicked(props.item)">
                <td class="subheading">{{ props.item.ftit }}</td>
              </tr>
            </template>

        </v-data-table>
      </v-flex>
    </v-layout>
    <v-layout row wrap v-else>
      <v-flex xs12>
        <p>Sem filmes associados</p>
      </v-flex>
    </v-layout>
  </v-container>
</template>







<script>
  import axios from 'axios'
  const lhost = "http://cinema.di.uminho.pt"

  export default{
    props: ["idAtor"],
    data:() =>({
      headers:[
        {text:'Titulo',align:'left',sortable:true,value:'title',class:'title'}
      ],
      filmes:[]
    }),
    mounted: async function() {
      try {
        var response = await axios.get(lhost + '/atores/' + this.idAtor + "/filmes")
        this.filmes = response.data
      } catch (error) {
        return error
      }
    },
    methods: {
      rowClicked: function(item){
        this.$router.push('/filmes/' + item.f.split('#')[1])
      }
    }
  }

</script>


<style>

</style>
