<template>
<div>
    <div class="discount">
        <h4>지금 결제하면 {{ discnt }}% 할인</h4>
    </div>
</div>
</template>

<script>
export default {
    name : 'TheDiscount',
    props : {
        discnt : Number,
    }
    

}
</script>

<style>

</style>