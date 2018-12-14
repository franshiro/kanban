<template>
  <div class="cardContent" data-toggle="modal" :data-target="'#'+item.id">
    <div class="card bg-primary text-white ">
        <h2>{{item.title}}</h2>
    </div>
    <detail :item="item" :name="name"></detail>
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
  props: ['item', 'name'],
  
  
}
</script>

<style scoped>
.cardContent {
  cursor: pointer;
  width: 90%;
  align-self: center;
  margin-bottom: 10px;
}
.card h2 {
  padding-top: 10px;
  padding-bottom: 10px;
  font-size: 20px;
}
</style>