<template>
  <div>
    <div v-for="(r,i) in room_detail" :key="r">
        <img :src="room_detail[i].image" class="room-img">
        <h4 @click="$emit('openModal',room_detail[i].id)">{{room_detail[i].title}}</h4>
        <p>{{room_detail[i].price}} 원</p>
    </div>
  </div>
</template>

<script>
export default {
    name : 'TheProducts',
    props: {
        room_detail : Array,
    }

} 
</script>

<style>

</style>