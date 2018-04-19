<template>
    <div class="container-fluid" @click="addtype_">
        <div class="row">
            <div class="col-md-6"><div class="pro_box" @click="text"><img src="https://placekitten.com/g/200/200" alt=""><div>进口牛油果</div><div>$1.00</div></div></div>
            <div class="col-md-6"><div class="pro_box"><img src="https://placekitten.com/g/200/200" alt=""><div>进口牛油果</div><div>$1.00</div></div></div>
            <div class="col-md-6"><div class="pro_box"><img src="https://placekitten.com/g/200/200" alt=""><div>进口牛油果</div><div>$1.00</div></div></div>
            <div class="col-md-6"><div class="pro_box"><img src="https://placekitten.com/g/200/200" alt=""><div>进口牛油果</div><div>$1.00</div></div></div>
        </div>
    </div>
</template>


<script>
    export default {
        data:function () {
            return{
             data:'我是第一个组件',
            }
        },
        methods:{
            text:function () {
                console.log('组件的事件');
            },
        }
    }
</script>