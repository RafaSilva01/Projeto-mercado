<!--Mexendo no back/adicionar item na tabela-->
<template>
  <div class="form-todo form-group">
  <span>
    <h6>Nome: </h6>
    <input placeholder="nome" type="text" name="author" class="form-control" v-model="name" />
  </span>
  <span>
    <h6>Email: </h6>
    <input placeholder="email" type="text" name="author" class="form-control" v-model="email" />
  </span>
  <span>
    <h6>Telefone: </h6>
    <input placeholder="telefone" type="number" name="author" class="form-control" v-model="number" />
  </span>
  <span>
    <h6>Mercadoria: </h6>
    <textarea placeholder="Mercadoria" name="message"  class="form-control" v-model="message"></textarea>
  </span>
  <br />
  <button v-on:click="addComment" type="submit" class="btn btn-success">Salvar</button>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        name: '',
        email:'',
        number:'',
        message: ''
      }
    },
    methods: {
      addComment() {
        if (this.message.trim() === '') {
          return;
        }
        this.$emit('add-todo', {
          name: this.name,
          email: this.email,
          number: this.number,
          message: this.message,
        });
        this.name = '';
        this.email = '';
        this.number = '';
        this.message = '';
      }
    }
  }
</script>
