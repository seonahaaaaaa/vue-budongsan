<template>
      <div>
        <!-- <transition name="fade"> -->
        <div class="start" :class="{end : modal_state}">
          <Modalpg @closeModal="modal_state = false;" :room_detail="room_detail" :clickNum="clickNum" :modal_state="modal_state" />
        </div>
      <!-- </transition> -->
        <div class="menu">
          <a v-for="menu in menu_name" :key="menu">{{ menu }}</a>
        </div>

      <Discountpg v-if="showDiscount == true" :discnt = "discnt"/>

     <button @click="priceSort()">가격순정렬</button>
     <button @click="priceUpSort()">가격역순정렬</button>
     <button @click="priceBack()">되돌리기</button>

      <Productspg @openModal="modal_state = true; clickNum = $event" :room_detail="room_detail" />

      </div>      
</template>

<script>
import TheModal from './Modal.vue'
import TheDiscount from './Discount.vue'
import oneroom from './post.js'
import Theproducts from './Products.vue'

export default {
  name: 'App',
  data() {
    return {
      showDiscount : true,
      modal_state : false,
      menu_name : ['Home', 'Products', 'About'],
      num : [0,0,0],
      room_detail: oneroom,
      room : [...oneroom],
      discnt : 30,
      // ... : 복사본 생성
      clickNum : 0,
      
    }
  },
  methods : {
    priceSort() {
      this.room_detail.sort(function(a,b){
        return a.price - b.price
        // 오브젝트형으로 a,b array에 해당되는 price 빼기
      });
    },
    priceBack() {
      this.room_detail = [...this.room]
    },
    priceUpSort() {
      this.room_detail.sort(function(a,b){
        return b.price-a.price
      });
    }
  },
  mounted() {
    setInterval(() => {
      this.discnt--;
    }, 1000);
  },
  components: {
    Discountpg : TheDiscount,
    Modalpg : TheModal,
    Productspg : Theproducts,

  }
}
</script>

<style>
/* .fade-enter-from {
  opacity: 0;
}

.fade-enter-active {
  transition: all 1s;
}

.fade-enter.to {
  opacity: 1;
} */

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.menu {
  background:  darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding : 10px;
}

body {
  margin :0
}

div {
  box-sizing: border-box;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}

.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}

.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding : 20px;
}

.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 20px;
}

.start {
  opacity: 0;
  transition: all 1s;

}

.end {
  opacity: 1;
}


</style>
