<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-md-12">
                <div>
                    <button class="btn btn-primary" data-toggle="modal" data-target=".bd-example-modal-lg">Large modal
                    </button>
                    <div class="modal fade bd-example-modal-lg" tabindex="-1" role="dialog"
                         aria-labelledby="myLargeModalLabel" aria-hidden="true">
                        <div class="modal-dialog modal-lg">
                            <div class="modal-content" v-for="item in productlist">
                                <div @click="bootest(item.id)">
                                    <img class="seleimg" :src="item.image" alt="">
                                    <span>{{item.name}}</span>
                                    <span>{{item.price}}</span>
                                    <span>{{item.symbol}}</span>
                                </div>
                            </div>
                        </div>
                    </div>

                </div>
            </div>
            <div class="col-md-4">
                <div class="box_">
                    <div class="box">
                        <div class="header1">12:00 AM</div>
                        <div class="header"><span class="hole3"></span><span class="hand"></span><span
                                class="hole1"></span></div>
                        <div class="header3"><i class="fa fa-signal icon"></i><i class="fa fa-wifi icon"></i><i
                                class="fa fa-battery-full icon"></i></div>
                        <div class="foot">
                            <div class="reca"></div>
                        </div>
                        <div class="container-fluid box_title"  v-for="n in showgoods">


                            <component :is="n"></component>

                        </div>

                    </div>
                </div>
            </div>
            <div class="col-md-8">
                <div class="box_type">

                </div>

                <input type="text" v-model="virproduct[0].name">
                <div class="box_type">
                    <div class="row">
                        <div class="col-md-2" v-for=" item in addtype">
                            <div class="box_type2" @click="typeclick(item.id)">
                                <i class="fa fa-plus"></i>
                                {{item.title}}
                            </div>
                        </div>
                    </div>
                    <div class="btn_box">
                        <button type="button" @click="con" class="btn btn-success">保存</button>
                        <button type="button" class="btn btn-warning">保存并预览</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    import axios from 'axios'
    import $ from 'jquery'
    import goods from './components-type/goods'
    import title_ from './components-type/title'

    export default {
        name: 'HelloWorld',
        data() {
            return {
                showgoods:[],
                virproduct:
                    [
                        {image:`https://placekitten.com/g/200/200`, name:'进口牛油果1', price:12000, symbol:'$',},
                        {image:`https://placekitten.com/g/200/200`, name:'进口牛油果2', price:12000, symbol:'$',},
                        {image:`https://placekitten.com/g/200/200`, name:'进口牛油果3', price:12000, symbol:'$',},
                        {image:`https://placekitten.com/g/200/200`, name:'进口牛油果4', price:12000, symbol:'$',},
                    ],
                //虚拟的展位商品
                showgoods: [],
                content: '',
                title: '123',
                addtype: [
                    {id: 1, title: '页面设置', click: 'proclick'},
                    {id: 2, title: '标题', click: "proclick"},
                    {id: 3, title: '商品', click: "proclick"},
                    {id: 4, title: '列表', click: "proclick"},
                    {id: 5, title: '商品搜索', click: "proclick"},
                    {id: 6, title: '图片导航', click: "proclick"},
                    {id: 7, title: '图片广告', click: "proclick"},
                    {id: 8, title: '富文本', click: "proclick"},
                    {id: 9, title: '自定义模板', click: "proclick"},
                    {id: 10, title: '商品列表', click: "proclick"},
                    {id: 11, title: '文本导航', click: "proclick"},
                    {id: 12, title: '分割线', click: "proclick"},
                    {id: 13, title: '辅助', click: "proclick"},
                    {id: 14, title: '空白', click: "proclick"},
                    {id: 15, title: '顶部菜单', click: "proclick"},
                    {id: 16, title: '橱窗', click: "proclick"},
                ],
                show: 0,
                showlist: false,
                productlist: [],
                proindexid:null,
            }
        },
        components: {
            goods: goods,
            title_:title_,
        },
        methods: {
            msg_type: function () {
                let box_type = document.querySelector('.box_type');
                box_type.innerHTML = this.goods_type;
            },
            title_type: function () {
                let box_type = document.querySelector('.box_type');
                box_type.innerHTML = this.title_type_;
            },
            typeclick: function (id) {
                this.show++;
                if (id == 1) {
                    this.proclick();
                }
                if (id == 2) {
                    this.titleclick()
                }
            },
            proclick: function () {
                this.showgoods.push('goods');
                // let box_title = document.querySelector('.box_title');
                // box_title.innerHTML += this.goods;
            },
            titleclick: function () {
                this.showgoods.push('title_');
                // let box_title = document.querySelector('.box_title');
                // box_title.innerHTML += this.title_;
            },
            con: function () {
                let box_title = document.querySelector('.box_title');
            },
            //隐藏状态框
            bootest: function (id) {
                let that=this;
                this.productlist.forEach(item => {
                    if (item.id==id){
                        console.log('that.proindexid',that.proindexid)
                        that.virproduct[that.proindexid].name="sdasdasd";
                    }
                })
                $('.modal').modal('hide')
            //    此时选择了商品,关闭了选择框,data中记录了选择模板的索引

            },

            clonetest:function () {
                $('.modal').modal('show')
            },
        },
        watch: {
            show: function () {
                let me = this;
                let type = document.querySelectorAll('.boxdele');
                type.forEach(item => {
                    item.addEventListener('mouseover', function () {
                        let su = item.querySelector('.su');
                        su.style.display = 'block';
                        //点击删除
                        su.addEventListener('click', function () {
                            let suu = su.parentNode;
                            suu.parentNode.removeChild(suu);
                        })
                    })

                    //鼠标移出,隐藏删除
                    item.addEventListener('mouseout', function () {
                        let su = item.querySelector('.su');
                        su.style.display = 'none';
                    })

                    //点击单个模板,显示出模板配置详情
                    item.addEventListener('click', function () {
                        let id = item.id;
                        if (id == 1) {
                            me.msg_type();
                        }
                        if (id == 2) {
                            me.title_type();
                        }
                    })


                    //    判断是哪个类型,模块内的内容实行不同的操作
                    if (item.id == 1) {
                        //    如果是商品,那么迭代这个商品数组
                        let pro_box = item.querySelectorAll('.pro_box');
                        pro_box.forEach(ban => {
                            ban.addEventListener('click', function () {
                                console.log('ban.id',ban.id)
                                me.proindexid=ban.id;
                                axios.get(`https://api4.yx8.tv/Commodity/list`).then(function (res) {
                                    let data = res.data.items;
                                    data.forEach(e => {
                                        e.image = `https://mp4.yx8.tv${e.image}`
                                    })
                                    me.productlist = data;
                                    //商品请求完毕以后启动商品选择框
                                    me.clonetest();
                                })
                            })
                        })
                    }
                })
            }
        },
        computed: {
            title_type_: function () {
                return `
                   <div class="row">
                <div class="col-md-12">
                这是一个标题信息框
                </div>
                </div>
                `
            },
            goods_type: function () {
                return `
                <div class="row">
                <div class="col-md-12">
                这是一个商品信息框
</div>
                </div>
                `
            },
            public: function () {
                return `
              <span class="dele">删除</span>
              `
            },
            goods: function () {
                //商品
                return `
<div class="row boxdele" id="1">
      <div class="col-md-6"><div class="pro_box" id="0"><img src="${this.virproduct[0].image}" alt=""><div>${this.virproduct[0].name}</div><div>${this.virproduct[0].symbol}${this.virproduct[0].price}</div></div></div>
      <div class="col-md-6"><div class="pro_box" id="1"><img src="${this.virproduct[1].image}" alt=""><div>${this.virproduct[1].name}</div><div>${this.virproduct[1].symbol}${this.virproduct[1].price}</div></div></div>
      <div class="col-md-6"><div class="pro_box" id="2"><img src="${this.virproduct[2].image}" alt=""><div>${this.virproduct[2].name}</div><div>${this.virproduct[2].symbol}${this.virproduct[2].price}</div></div></div>
      <div class="col-md-6"><div class="pro_box" id="3"><img src="${this.virproduct[3].image}" alt=""><div>${this.virproduct[3].name}</div><div>${this.virproduct[3].symbol}${this.virproduct[3].price}</div></div></div>
      <div class="col-md-12 su">${this.public}</div>
</div>
      `
            },
            title_: function () {
                return `
<div class="row boxdele" id="2">
<div class="col-md-12">${this.title}</div>
<div class="col-md-12 su">${this.public}</div>
</div>
                `
            }


        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .box_ {
        margin: 0 auto;
        margin-top: 50px;
        position: relative;
        width: 300px;
        height: 600px;
        border-radius: 50px;
        overflow: hidden;
        /*border: 10px solid rgba(0,0,0,0);*/
    }

    .box {
        width: 300px;
        height: 600px;
        /*margin: 0 auto;*/
        border: 10px solid black;
        /*margin-top: 50px;*/
        border-radius: 50px;
        /*position: relative;*/
        overflow: auto;
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
