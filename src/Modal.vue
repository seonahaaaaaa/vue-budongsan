<template>
    <div>
        <div class="black-bg" v-if="modal_state==true">
          <div class="white-bg">
            <img :src="room_detail[clickNum].image" class="room-img">
            <h4>{{room_detail[clickNum].title}}</h4>
            <p>{{room_detail[clickNum].content}}</p>
            <input type="text" v-model.number="month">
            <!-- 사용자가 input에 저장한 text는 number형으로 초기화해두어도 문자로 저장됨 => v-model.number 로 받으면 숫자형으로 변환 -->
            <p>{{ month }}개월 : {{month*room_detail[clickNum].price}} 원</p>
            <Discountpg/>
            <button @click="$emit('closeModal')">닫기</button>
          </div>
        </div>

    </div>
</template>

<script>
export default {
    name : 'TheModal',
    data() {
      return {
        month : 1,

      }
    },
    props: {
        room_detail : Array,
        clickNum : Number,
        modal_state : Boolean,
    },
    watch : {
      // 함수명 선언 시, 선언한 data명이랑 동일하게 입력해야함
      month(num) {
        // month라는 데이터가 변할때마다 여기있는 코드 실행됨 (코드 감시 개념)
        if(num > 13) {
          alert("13개월 이상은 입력 불가합니다.");
          this.month = '';
        };
        const notPhoneticSymbolExp = /[ㄱ-ㅎ|ㅏ-ㅣ|가-힣]/;
        if(notPhoneticSymbolExp.test(num)){
          alert("숫자만 입력해주세요.");
          this.month = '';
        };

      },

    }
}
</script>

<style>

</style>