<template>
  <div class="cardContent">
    <div class="card bg-primary text-white ">
        <h2>{{item.title}}</h2>
    </div>
      <h6>Assigned to : {{item.to}}</h6>
    <div class="container-button">
      <div>
        <button class="btn btn-success" data-toggle="modal" :data-target="'#'+item.id">Detail</button>
      </div>
      <div>
        <button class="btn btn-danger" @click="removeItem">Delete</button>
      </div>
      <div>
        <button class="btn btn-secondary" @click="actionOne">{{buttonOne}}</button>
      </div>
      <div>
        <button class="btn btn-secondary" @click="actionTwo" v-if="buttonTwo">{{buttonTwo}}</button>
      </div>
    </div>
    <detail :item="item"></detail>
  </div>
</template>

<script>
import database from '../assets/config.js'
import detail from '@/components/detail.vue'
export default {
  name: 'content',
  components : {
    detail
  },
  data: function () {
    return {
      buttonOne: '',
      buttonTwo: '',
      toModal : '#' + this.item
    }
  },
  props: ['item', 'name'],
  methods: {
    actionOne () {
      database.ref(`/${this.item.id}`).remove()
      database.ref('/').push({
        title: this.item.title,
        description : this.item.description,
        point : this.item.point,
        to : this.item.to,
        status: this.buttonOne
      })
    },
    actionTwo () {
      database.ref(`/${this.item.id}`).remove()
      database.ref('/').push({
        title: this.item.title,
        description : this.item.description,
        point : this.item.point,
        to : this.item.to,
        status: this.buttonTwo
      })
    },
    removeItem () {
      database.ref(`/${this.item.id}`).remove()
    }
  },
  created () {
    if (this.name === 'Pre-Log') {
      this.buttonOne = 'To-Do'
      this.buttonTwo = null
    } else if (this.name === 'To-Do') {
      this.buttonOne = 'Pre-Log'
      this.buttonTwo = 'On-Going'
    } else if (this.name === 'On-Going') {
      this.buttonOne = 'Finished'
      this.buttonTwo = 'To-Do'
    } else if (this.name === 'Finished') {
      this.buttonOne = 'On-Going'
      this.buttonTwo = null
    }
  }
}
</script>

<style scoped>
.cardContent {
  font-size: 10px;
  color: black;
  width: 70%;
  min-height: 100px;
  background-color: #c2c4c7;
  -webkit-box-shadow: 0px 5px 4px #c0c0c09d;
  -moz-box-shadow: 0px 5px 4px #c0c0c09d;
  box-shadow: 0px 5px 4px #c0c0c09d;
  border-radius: 5px;
  margin-left: auto;
  margin-right: auto;
  text-align: center;
  margin-bottom: 50px;
  vertical-align: middle;
  cursor: pointer;
  padding-bottom: 20px;
}
.card h2 {
  padding-top: 20px;
  font-size: 20px;
}
.container-button h4 {
  color: #4684f6;
  background-color: #fff;
  margin-left: auto;
  margin-right: auto;
  text-align: center;
  width: 30%;
  padding: 2%;
  border-radius: 5px;
}
</style>