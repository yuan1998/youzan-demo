<template>
    <div class="container-fluid par">
        <div class="row">
            <div class="col-md-6"><div class="pro_box" @click="text"><img src="https://placekitten.com/g/200/200" alt=""><div>进口牛油果</div><div>$1.00</div></div></div>
            <div class="col-md-6"><div class="pro_box"><img src="https://placekitten.com/g/200/200" alt=""><div>进口牛油果</div><div>$1.00</div></div></div>
            <div class="col-md-6"><div class="pro_box"><img src="https://placekitten.com/g/200/200" alt=""><div>进口牛油果</div><div>$1.00</div></div></div>
            <div class="col-md-6"><div class="pro_box"><img src="https://placekitten.com/g/200/200" alt=""><div>进口牛油果</div><div>$1.00</div></div></div>
        </div>
        <div class="son">
            <div class="box">
                <div>
                    <button class="" @click="test"></button>

                </div>
            </div>
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

<style scoped>
    .par{
        /*position: relative;*/
    }
    .son{
        position: fixed;
        /*left: 100%;*/
        top: 25%;
        right: 25%;
    }
    .box{
        background-color: red;
        z-index: 100;
        width: 200px;
        height: 200px;
    }
</style>