<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-md-12">
                <div>
                </div>
            </div>
            <div class="col-md-4">
                <div class="box_">
                    <div class="box">
                        <div class="container-fluid box_title"  v-for="(item ,n) in range">
                            <div class="component-wrapper" @click="focusComponent(n)" :class="{'_focus':focusC == n}">
                                <component :is="item.name" :index="n" :data="item.data" @changeData="changeData"></component>
                                <div class="component-controls">
                                    <div class="btn-item" @click.self="upRecord(n)">
                                        Up
                                    </div>
                                    <div class="btn-item" @click.self="downRecord(n)">
                                        Down
                                    </div>
                                    <div class="btn-item" @click.self="removeComponent(n)">
                                        remove
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col-md-8">
                <div class="box_type">
                </div>
                <div class="box_type">
                    <div class="row">
                        <div class="col-md-2" v-for=" item in addtype">
                            <div class="box_type2" @click="addComponent(item.component)">
                                <i class="fa fa-plus"></i>
                                {{item.title}}
                            </div>
                        </div>
                    </div>
                    <div class="btn_box">
                        <button type="button"  class="btn btn-success">保存</button>
                        <button type="button" class="btn btn-warning">保存并预览</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .box_ {
        margin: 0 auto;
        margin-top: 50px;
        position: relative;
        width: 300px;
        height: 600px;
        /*border: 10px solid rgba(0,0,0,0);*/
    }

    .box {
        width: 300px;
        height: 600px;
        /*margin: 0 auto;*/
        /*margin-top: 50px;*/
        /*position: relative;*/
        padding-top: 33px;
    }

    /*.header,.header1,.header3{*/
    /*display: inline-block;*/
    /*}*/
    .header span {
        display: inline-block;
    }

    .header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 0 15px;
        color: #fff;
        height: 30px;
        width: 140px;
        margin: 0 auto;
        background-color: #000;
        border-bottom-left-radius: 20px;
        border-bottom-right-radius: 20px;
        position: absolute;
        top: 6px;
        left: 27%;
    }

    .hand {
        height: 8px;
        width: 60px;
        background-color: #999;
        border-radius: 5px;

    }

    .hole1 {
        height: 12px;
        width: 12px;
        border-radius: 6px;
        background-color: #031236;
        box-shadow: 0px 0px 2px #ddd inset;
    }

    .hole3 {
        height: 8px;
        width: 8px;
        border-radius: 4px;
        background-color: #2C2C2C;
    }

    .header1, .header3 {
        position: absolute;
        background-color: rgb(141, 187, 227);
        top: 7px;
        width: 150px;
        height: 33px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        z-index: -10;
    }

    .header1 {
        left: 3px;
        color: #fff;
        font-size: 10px;
        padding-left: 22px;
        border-top-left-radius: 80px;
    }

    .header3 {
        padding: 0 23px 0 73px;
        right: 3px;
        border-top-right-radius: 90px;
    }

    .foot {
        position: absolute;
        padding-right: 20px;
        width: 100%;
        bottom: 0;
        display: flex;
    }

    .reca {
        margin: 0 auto;
        height: 10px;
        width: 130px;
        background-color: #999;
        border-radius: 5px;
        margin-bottom: 22px;
    }

    .icon {
        color: #fff;
        font-size: 10px;
    }

    .box_type {
        position: fixed;
        bottom: 0;
    }

    .box_type2 {
        cursor: pointer;
        margin: 5px;
        padding: 3px;
        text-align: center;
        border-radius: 5px;
        transition: 1s;
        background-color: rgb(247, 247, 247);
    }

    .box_type2:hover {
        background-color: rgb(197, 197, 197);
    }

    .btn_box {
        text-align: center;
        margin: 20px 0;
        margin-bottom: 40px;
    }

    .seleimg {
        width: 100px;
        height: 80px;
    }


    .component-wrapper {
        border:2px;
        border-color:transparent;
        position: relative;
    }

    .component-wrapper._focus {
        border:2px dashed #27A343;
    }

    .component-wrapper .component-controls {
        visibility: hidden;
        position :absolute;
        bottom: 0;
        right: 0;
    }

    .component-wrapper._focus .component-controls {
        visibility:visible;
    }

    .component-wrapper._focus .component-controls .btn-item {
        display: inline-block;
        color:#f8f8f8;
        font-size: 10px;
        line-height: 18px;
        padding-left: 10px;
        padding-right: 10px;
        background: rgba(0,0,0,.7);
        border-top-left-radius: 5px;
        border-top-right-radius: 5px;
    }


    .component-wrapper._focus >>> .son {
        visibility: visible;
    }

</style>

<style>

    .col-md-6 {
        margin: 0;
        padding: 0;
    }

    .pro_box {
        margin: 0;
        padding: 0 10px 5px 10px;
    }

    .pro_box img {
        width: 100%;
        height: 135px;
    }

    .boxdele:hover {
        border: 3px dashed red;
    }

    .su {
        display: none;
    }

    .suu {
        display: inline-block;
    }

</style>


<script>
    import axios from 'axios'
    import $ from 'jquery'
    import goods from './components-type/goods'
    import title_ from './components-type/title'

    export default {
        name: 'HelloWorld',
        data() {
            return {
                title: '123',
                focusC:null,
                componentTypes:{
                    goods:{
                        name:'goods',
                        data:{
                            style:{
                                layout:1
                            },
                            content:[],
                            priceShow:false,
                            titleShow:false,
                            cartShow:false
                        },
                    },
                    title_:{
                        name:'title_',
                        data:{
                            title:'',
                            textAlign:'center',
                            subtitle:''
                        }
                    }
                },
                range:[],
                addtype: [
                    {id: 1, title: '页面设置', component: 'goods'},
                    {id: 2, title: '标题', component: "title_"},
                    {id: 3, title: '商品', component: "goods"},
                    {id: 4, title: '列表', component: "goods"},
                    {id: 5, title: '商品搜索', component: "goods"},
                    {id: 6, title: '图片导航', component: "goods"},
                    {id: 7, title: '图片广告', component: "goods"},
                    {id: 8, title: '富文本', component: "goods"},
                    {id: 9, title: '自定义模板', component: "goods"},
                    {id: 10, title: '商品列表', component: "goods"},
                    {id: 11, title: '文本导航', component: "goods"},
                    {id: 12, title: '分割线', component: "goods"},
                    {id: 13, title: '辅助', component: "goods"},
                    {id: 14, title: '空白', component: "goods"},
                    {id: 15, title: '顶部菜单', component: "goods"},
                    {id: 16, title: '橱窗', component: "goods"},
                ],
            }
        },
        components: {
            goods,
            title_
        },
        methods: {
            newObj(obj) {
                return JSON.parse(JSON.stringify(obj));

            },
            addComponent(name) {
                this.range.push(this.newObj(this.componentTypes[name]));
                this.focusC = this.range.length - 1;
            },
            removeComponent(index) {
                return this.range.splice(index,1);
            },
            recordComponent(index, nIndex) {
                let _cache = this.removeComponent(index)[0];
                this.range.splice(nIndex,0,_cache);
                console.log(this.focusC);
                this.focusC = nIndex;
                console.log(this.focusC);
            },
            upRecord(index) {
                if(index == 0)
                    return ;
                this.recordComponent(index , index - 1);
            },
            downRecord(index) {
                if(index == this.range.length - 1 )
                    return ;

                this.recordComponent(index , index + 1);
            },
            changeData(index,data) {
                console.log(index,data);
                this.range[index].data = data;
            },
            focusComponent(index) {
                this.focusC = index;
            }
        },
        computed: {



        }
    }
</script>
