<template>
  <div class="formulario">
    <lista
      titulo="Filmes"
      :items="getFilmes"
      @editar="editar" 
      @deletar="deletar"
      @inserir="inserir"
    />
  </div>
</template>

<script>
import {mapGetters, mapActions, mapMutations} from 'vuex'
export default {
  computed:{
    ...mapGetters([
      'getFilmes'
    ])
  },
  data(){
    return{
      videos:[]
    }
  },
  created(){
    this.buscarFilmes()
  },
  methods:{
    ...mapActions([
      'buscarFilmes',
      'excluirFilme',
    ]),
    ...mapMutations([
      'setFilme'
    ]),
    inserir(){
      this.setFilme({});
      this.$router.push("filme-cadastro")
    },  
    editar(filme){
      this.setFilme(filme);
      this.$router.push("filme-cadastro");
    },
    deletar(filme) {
         this.excluirFilme(filme)
        .then( ({ data } ) => {
          alert(data);
        }) 
    },
  }
}
</script>