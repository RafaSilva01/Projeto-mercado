<!--Aqui faz aparecer as informações na tela-->
<template>
    <commentsList/>
    
</template>
<!--sempre que criar uma nova pasta tem que adicionar um import/exportar/ e colocar no template-->
<script>
  import commentsList from './components/commentsList'


  export default{
    name: 'app',
    components: {
      commentsList
    },

    data(){
      return{
    }
  }
  }
</script>




