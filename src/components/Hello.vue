<template>


  <div class="container">
    <header-component></header-component>

    <todo-list-component></todo-list-component>

    <footer-component></footer-component>
  </div>


</template>

<script>
  import HeaderComponent from "./Header";
  import FooterComponent from "./Footer";
  import TodoListComponent from "./TodoList";

  export default {
    components: {
      FooterComponent,
      HeaderComponent,
      TodoListComponent
    },
    name: 'hello',
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
