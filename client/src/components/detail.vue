<template>
  <div class="modal fade" :id="item.id" tabindex="-1" role="dialog" aria-labelledby="detailTask" aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered modal-md" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">{{item.title}}</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <form>
            <div>
              <p> Description : {{item.description}}</p>
              <p>Point : {{item.point}}</p>
              <p>Assigned to : {{item.to}}</p>
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
  props : ['item'],
  data(){
    return {
      title : '',
      description : '',
      point : 0,
      to : ''
    }
  },
}
</script>

<style>

</style>
