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
            <table class="table-detail">
              <tbody>
                <tr class="border">
                  <td>Description</td>
                  <td>:</td>
                  <td>{{item.description}}</td>
                </tr>
                <tr class="border">
                  <td>Point</td>
                  <td>:</td>
                  <td>{{item.point}}</td>
                </tr>
                <tr class="border">
                  <td>Assigned to</td>
                  <td>:</td>
                  <td>{{item.to}}</td>
                </tr>
              </tbody>
            </table>
          <div class="container-button d-flex">
            <div class="mr-auto p2">
              <button class="btn btn-danger" @click="removeItem" data-dismiss="modal">
                <span class="fas fa-trash-alt"></span>
              </button>
            </div>
            <div class="p2">
              <button class="btn btn-secondary" v-if="buttonOne" @click="actionOne" data-dismiss="modal">
                <span class="fas fa-hand-point-left"></span> {{buttonOne}}
              </button>
            </div>
            <div class="p2">
              <button class="btn btn-secondary" @click="actionTwo" v-if="buttonTwo" data-dismiss="modal">
                {{buttonTwo}} <span class="fas fa-hand-point-right"></span>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import database from '../assets/config.js'
export default {
  props : ['item', 'name'],
  data : function(){
    return{
      buttonOne: '',
      buttonTwo: '',
    }
  },
  methods: {
    actionOne () {
      database.ref(`/todo/${this.item.id}`).remove()
      database.ref('/todo').push({
        title: this.item.title,
        description : this.item.description,
        point : this.item.point,
        to : this.item.to,
        status: this.buttonOne
      })
    },
    actionTwo () {
      database.ref(`/todo/${this.item.id}`).remove()
      database.ref('/todo').push({
        title: this.item.title,
        description : this.item.description,
        point : this.item.point,
        to : this.item.to,
        status: this.buttonTwo
      })
    },
    removeItem () {
      database.ref(`/todo/${this.item.id}`).remove()
    }
  },
  created () {
    if (this.name === 'Pre-Log') {
      this.buttonOne = null
      this.buttonTwo = 'To-Do'
    } else if (this.name === 'To-Do') {
      this.buttonOne = 'Pre-Log'
      this.buttonTwo = 'On-Going'
    } else if (this.name === 'On-Going') {
      this.buttonOne = 'To-Do'
      this.buttonTwo = 'Finished'
    } else if (this.name === 'Finished') {
      this.buttonOne = 'On-Going'
      this.buttonTwo = null
    }
  }
 
}
</script>

<style>
  .table-detail{
    border: 1px solid black;
    width: 100%;
    margin-bottom : 20px;
    font-size: 16px;
  }
  .border{
    border: 1px solid black;
  }
</style>
