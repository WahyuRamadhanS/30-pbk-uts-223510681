<template>
  <div class="container">
    <!-- Header with menu -->
    <header class="header">
      <div class="logo-container">
        <img class="logo" src="./logo1.png">
        <h1 class="app-name">Todo & Post</h1>
      </div>
      <nav class="menu">
        <ul>
          <li @click="pilihMenu('todos')" :class="{ 'aktif': menuAktif === 'todos' }">Todos</li>
          <li @click="pilihMenu('post')" :class="{ 'aktif': menuAktif === 'post' }">Post</li>
        </ul>
      </nav>
    </header>
    
    <!-- Content depending on the selected menu -->
    <div class="konten">
      <div v-if="menuAktif === 'todos'">
        <!-- TodoList component with custom slot content -->
        <Todos>
          <template #create-todo-extra>
            <p>This is extra content in the create activities section.</p>
          </template>
        </Todos>
      </div>
      <div v-else-if="menuAktif === 'post'">
        <!-- Post component with selected user ID and custom slot content -->
        <Post :selectedUserId="selectedUserId">
          <template #custom-content>
            <p>This is custom content displayed above the post list.</p>
          </template>
        </Post>
      </div>
    </div>
  </div>
</template>

<script>
import Todos from './components/todos.vue'; 
import Post from './components/post.vue'; 

export default {
  components: {
    Todos,
    Post
  },
  data() {
    return {
      menuAktif: 'todos',
      selectedUserId: null // You can set this dynamically based on your requirements
    };
  },
  methods: {
    pilihMenu(menu) {
      this.menuAktif = menu;
    }
  }
};
</script>

<style scoped>
/* Container styles */
.container {
  padding-top: 0px; /* Gap between header and content */
  padding-bottom: 20px;
}

/* Header styles */
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  padding-bottom: 10px; /* Added padding at   the bottom of the header */
  background-color: #102C57;
  color: #FEFAF6;
  border-radius: 5px;
  border-bottom: 3px solid #fc2121; /* Bottom border on the header */
  padding: 10px 20px 20px;
  font-size: larger;
}

.logo-container {
  display: flex;
  align-items: center;
}

.logo {
  width: 75px;
  height: 75px;
  margin-right: 10px;
}

.app-name {
  font-size: 24px;
  margin: 0;
}

.menu ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  display: flex;
}

.menu ul li {
  margin-right: 30px;
  cursor: pointer;

}

.menu ul li.aktif {
  font-weight: bold;
}
</style>

