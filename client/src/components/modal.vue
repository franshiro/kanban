<template>
  <div class="modal fade" id="modalAddTodo" tabindex="-1" role="dialog" aria-labelledby="modalAddTodo" aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered modal-md" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">New Task</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <form>
            <div class="form-row">
              <div class="form-group col-md-12">
                <label>Title</label>
                <input type="text" class="form-control" v-model="title"  placeholder="Title ... ">
              </div>
              <div class="form-group col-md-12">
                <label>Description</label>
                <input type="text" class="form-control" v-model="description"  placeholder="Description ... ">
              </div>
              <div class="form-group col-md-12">
                <label>Point</label>
                <input type="text" class="form-control" v-model="point">
              </div>
              <div class="form-group col-md-12">
                <label>Assigned To</label>
                <input type="text" class="form-control" v-model="to"  placeholder="to ... ">
              </div>
            </div>
          </form>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-primary"  data-dismiss="modal" @click="addTask">Add Task</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import database from '../assets/config.js'
export default {
  data(){
    return {
      title : '',
      description : '',
      point : 0,
      to : ''
    }
  },
  methods : {
    addTask(){
        database.ref('/').push({
        title: this.title,
        description : this.description,
        point : this.point,
        to : this.to,
        status: 'Pre-Log'
      })
      this.title = ''
      this.description = '',
      this.point = 0
      this.to = ''

    }
  }
}
</script>

<style>

</style>
