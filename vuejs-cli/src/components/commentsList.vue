<!--Mexendo com o front/imagens/estilo da pagina-->
<template>
 <div class="p-3 mb-2 bg-info">
  <div class="container">
    <div class="p-3 mb-2 bg-warning text-dark"> 
    <h2>Mercadorias</h2>
    </div>
  <v-carousel :show-arrows="false">
    <v-carousel-item
      v-for="(item,i) in items"
      :key="i"
      :src="item.src"
    ></v-carousel-item>
  </v-carousel>
  <br/>    
    <div class="p-3 mb-2 bg-warning text-dark">
      <h1>Cadastro</h1>
      </div>
    <br />

<!--o add todo e responsavel por puxar as informações do back end e trazer pro front-->
      <FormTodo v-on:add-todo="addComment"></FormTodo>
        <div class="list-group bg-transparent">
          <p v-if="comments.length <= 0">Sem cadastro</p>
        </div>
    <br />
    <br /> 
    <br />
    <div class="p-3 mb-2 bg-warning text-dark"> 
    
    <h2>Tabela</h2>
    </div>
    <v-data-table
      :headers="headers"
      :items="comments"
      :items-per-page="5"
      class="elevation-1"
    ></v-data-table>
    <br />
    <button>
        <a href="#" title="Excluir" v-on:click.prevent="removeComment(index)"  type="submit" class="btn btn-danger">Excluir</a>
    </button>    
  </div>
</div>
</template>

<!--script, onde e definido e exportado pra tela-->
<script>
import FormTodo from './FormTodo';
import {http} from '../services/config';

export default {
  components: {
    FormTodo
  },
  data() {
    return {
      comments: [],

       //Tabela e fotos
       headers: [
          {
            text: 'Nome',
            align: 'start',
            sortable: false,
            value: 'name',
          },
          { text: 'Email', value: 'email' },
          { text: 'Telefone', value: 'number' },
          { text: 'Mercadoria', value: 'message' },   
        ],
        items: [
          {
            src: 'https://www.sabornamesa.com.br/media/k2/items/cache/dee4183b3eece6f1f1fda5b7115d2824_XL.jpg',
          },
          {
            src: 'https://www.infoescola.com/wp-content/uploads/2011/02/carne-vermelha-450x324.jpg',
          },
          {
            src: 'https://70096.cdn.simplo7.net/static/70096/sku/queijos-parmesao-queijo-parmesao-capa-preta--p-1635522224895.jpg',
          },
          {
            src: 'https://institucional.hortifruti.com.br/wp-content/uploads/2016/07/Batata-1.jpg',
          },
          {
            src: 'https://jbchost.com.br/ht/wp-content/uploads/2016/12/videoarroz.jpg',
          },
          {
            src: 'https://1.bp.blogspot.com/-elJqjqlbYuo/XwJZ5Hk4ukI/AAAAAAAABYs/9hGJf4xD9l0cDrAZiV2L_MCKjmUWMgsmgCLcBGAsYHQ/s1600/Feij%25C3%25A3o%2B1.jpg',
          },
          {
            src: 'https://www.meon.com.br/source/files/originals/meon_menu_macarrao_abobrinha-824066.jpg',
          },
        ],

    }
  },
  methods: {

    //recebe comentario,adiciona na lista e manda salvar
    addComment(comment) {
      this.salvar(comment);
      window.location.reload();
    },
    removeComment(index) {
      this.comments.splice(index, 1);

    },

    //manda requisição post com o comentario recebido
    salvar(comentario){
        http.post('usuarios/', comentario) 
        
        //trabalha com a reposta da requisição
        .then(() =>{
            alert('Salvo com sucesso!!!')
        })
        //trabalha com a tratativa de error

        .catch (function (error){
          if (error.response) {
            console.log(error.response.data);
            console.log(error.response.headers);
            alert('Não cadastrado');
              
            } 
        });
        
      },
    apagar(index){
        http.post('usuarios/', index);
        alert('Deletado com sucesso!!!')
    },
    listar(){
      http.get('usuarios/').then(resposta => {
        this.comments = resposta.data;   
      })
    }
  },
  mounted(){
    this.listar();
  },
  /*computed: {
    allComments() {
      return this.comments.map(comment => ({
        ...comment,
        name: comment.name.trim() === '' ? 'Anônimo' : comment.name
      }))
    }
  },*/
  watch: {
    comments(val) {
      console.log('val', val)
    }
  }
}
</script>