<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark fixed-top">
        <h1>Kanban</h1>
        <div class="ml-auto my-2 my-lg-0">
          <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#modalAddTodo">Add</button>
        </div>
    </nav>  
  <modalAdd></modalAdd>
  </div>
</template>

<script>
import database from '../assets/config.js'
import modalAdd from '@/components/modal.vue'
export default {
  name: 'navbar',
  components :{
    modalAdd
  },
  data () {
    return {
      title: '',
      description : '',
      point : '',
      to : '' 
    }
  },
  methods: {
    sendItem () {
      database.ref('/').push({
        title: this.item.title,
        description : this.item.description,
        point : this.item.point,
        to : this.item.point,
        status: 'Pre-Log'
      })
      this.taskName = ''
    }
  }
}
</script>

<style scoped>
html,
body {
  font-family: 'Lato';
  margin: 0;
  padding: 0;
  overflow-x: hidden;
}
h1,
h2,
h3 {
  padding: 0;
  margin: 0;
  color : white;
}

input {
  height: 30px;
  width: 300px;
  margin-bottom: 20px;
  margin-top: 20px;
  border-radius: 5px;
}
</style>