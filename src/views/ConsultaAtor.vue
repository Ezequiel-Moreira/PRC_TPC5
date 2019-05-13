<template>
	<v-container>
    <MetaAtor :idAtor="$route.params.id"/>
    <Filmes :idAtor="$route.params.id"/>
    <v-layout>
      <v-btn @click="goBack" color="info">Voltar à página anterior</v-btn>
    </v-layout>
  </v-container>
</template>

<script>
	import MetaAtor from '@/components/AtorMeta'
	import Filmes from '@/components/AtorFilmes'

	export default {
		components: {
			MetaAtor,Filmes
    },
    methods: {
      goBack: function(){
        this.$router.go(-1)
      }
    }
	}
</script>
