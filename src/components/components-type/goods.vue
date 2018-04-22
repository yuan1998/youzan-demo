<template>
    <div class="container-fluid par">
        <div class="row">
            <template v-for="(item,n) in productContent">
                <div :class="productStyle">
                    <div class="pro_box">
                        <img :src="item.imageUrl" alt="">
                        <div v-if="selfData.titleShow">{{item.name}}</div>
                        <div v-if="selfData.priceShow">{{item.price}}</div>
                    </div>
                </div>
            </template>
        </div>
        <div class="son">
            <div class="box">
                <div class="panel-wrap">
                    <div class="panel-bar">
                        <div class="panel-body">
                            <div class="panel-style">
                                <div class="style-row">
                                    商品样式
                                    <label >
                                        样式一
                                        <input type="radio" value="lg" v-model="selfData.style.layout">
                                    </label>
                                    <label >
                                        样式二
                                        <input type="radio" value="sm" v-model="selfData.style.layout">
                                    </label>
                                </div>
                                <div class="other-row">
                                    显示内容
                                    <div>
                                        <div>
                                            <label >
                                                显示标题
                                                <input type="checkbox" v-model="selfData.titleShow">
                                            </label>
                                        </div>
                                        <div>
                                            <label >
                                                显示价格
                                                <input type="checkbox" v-model="selfData.priceShow">
                                            </label>
                                        </div>
                                        <div>
                                            <label >
                                                显示购物车按钮
                                                <input type="checkbox" v-model="selfData.cartShow">
                                            </label>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>


<script>
    export default {
        props:{
            data:Object,
            index:Number
        },
        data() {
            return{
                selfData:this.data,
            }
        },
        computed: {
            productStyle() {
                let style = this.selfData.style,
                    layout = style.layout;

                if(layout == 1)
                    return 'col-sm-12';
                else if (layout == 2)
                    return 'col-sm-6';
            },
            productContent() {
                let content = this.selfData.content,
                    _cache;

                if(content.length < 3){
                    for(let i = content.length;i<3;i++){
                        _cache = {
                            name:'商品' + i,
                            price: i +'.000',
                            imageUrl:'https://placekitten.com/g/200/200'
                        }
                        content.push(_cache);
                    }
                }

                return content;
            }
        },
        watch:{
            selfData: {
                handler(val) {
                    console.log('组件数据修改了');
                    this.$emit('changeData',this.index,val);
                },
                deep:true
            },
            data(val) {
                console.log('页面数据修改了');
                if(this.selfData == val)
                    return ;
                this.selfData == val;
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
        position: relative;
    }
    .son {
        visibility: hidden;
        position:absolute;
        top: 0;
        left:110%;
        width: 600px;
        height: 600px;
        z-index: 50;
    }

</style>