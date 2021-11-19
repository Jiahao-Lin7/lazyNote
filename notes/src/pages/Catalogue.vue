<template>
    <div id="catelogue">
        <div class="pic_box">
            <div id="myChart" :style="{width: '500px', height: '500px'}"></div>
            <div v-for="(item,index) in arr" :key="index" :id="item.id" :style="{width: '500px', height: '500px'}">
            {{item}}
            </div>
        </div>
        <div class="box">
            <div class="title" >{{title}}</div>
            <div class="context" v-html="context"></div>
        </div>
        <!-- <div>{{this.title}}{{this.context}}</div> -->
        <!-- <div id="" class="">{{this.$route.params.obj}}</div> -->
    </div>
    
</template>

<script>
import {mapState} from "vuex";
import E from "wangeditor";
    export default {
        name: 'Catelogue',
        mounted() {
            this.drawLine();
            // this.editor = new E("#editor");
            // this.editor.config.uploadImgShowBase64 = true;
            // this.editor.config.showLinkImg = false;
            // this.editor.create();
            // this.editor.txt.html();
            this.title = this.titleVuex;
            // this.editor.txt.html(`${this.contextVuex}`)
        },
        computed:{
                  ...mapState(['note']),
                  titleVuex(){
                    return this.$store.state.title;
                  },
                  contextVuex(){
                    return this.$store.state.context;
                  }
                },
        data() {
            return {
                //title: this.$route.params.title,
                obj:this.$route.params.obj,
                //context:this.contextVuex,
                // context: this.$router.params.context,
                jsonData:'',
                context:'',
                editor: "",
                title: "",
                userid: "",
                input:'',
                myChart: '',
                syncData: '',
                now: '',
                data: '',
                arr: [{
                    name: 'vue',
                    id: 'echart0',
                    children: [{
                        name: '新建文件夹'
                    }, {
                        name: 'vuex',
                        children: [{
                            name: '显示笔记'
                        }, {
                            name: '新建笔记'
                        }]
                    }]
                }, {
                    name: 'react',
                    id: 'echart1',
                    children: [{
                        name: '新建文件夹'
                    }, {
                        name: '生命周期',
                        children: [{
                            name: '显示笔记'
                        }, {
                            name: '新建笔记'
                        }]
                    }]
                }]
            }
        },
        methods: {
            open() {
                this.$alert(  <input placeholder = "请输入笔记名称" id="content"></input>, '添加笔记', {
                    confirmButtonText: '确定',
                    callback: () => {
                        let content = document.getElementById('content');
                        console.log(content);
                        this.syncData = content.value
                        if(content.value != '') {
                            this.add();
                            this.$message({
                            type: 'info',
                            message: `添加成功`
                            });
                            this.syncData = ''
                            content.value = ''
                            console.log(content);
                        } else {
                             console.log(content);
                            this.$message({
                            type: 'info',
                            message: `添加失败`
                           
                            });
                        }
                    }
                });
        },
        add() {
            let myChart = this.$echarts.init(document.getElementById('myChart'))
            this.data.children.push({
                name: this.syncData,
                children: [{name:'显示笔记'},{name:'新建笔记'}]
            })
            let a = this.data;
            myChart.setOption({
                tooltip: {
                    trigger: 'item',
                    triggerOn: 'mousemove'
                },
                series: [{
                    type: 'tree',
                    id: 0,
                    name: 'tree1',
                    data: [a],
                    top: '10%',
                    left: '8%',
                    bottom: '22%',
                    right: '20%',
                    symbolSize: 7,
                    edgeShape: 'polyline',
                    edgeForkPosition: '63%',
                    initialTreeDepth: 3,
                    lineStyle: {
                        width: 2
                    },
                    label: {
                        backgroundColor: '#fff',
                        position: 'left',
                        verticalAlign: 'middle',
                        align: 'right'
                    },
                    leaves: {
                        label: {
                            position: 'right',
                            verticalAlign: 'middle',
                            align: 'left'
                        }
                    },
                    emphasis: {
                        focus: 'descendant'
                    },
                    expandAndCollapse: true,
                    animationDuration: 550,
                    animationDurationUpdate: 750
                }]
            });
        },
        drawLine() {
            let myChart1; // eslint-disable-line no-unused-vars
            for (let i = 0; i < this.arr.length; i++) {
                myChart1 = 'myChart' + i;
                let id = 'echart' + i;
                myChart1 = this.$echarts.init(document.getElementById(id))
                myChart1.setOption({
                    tooltip: {
                        trigger: 'item',
                        triggerOn: 'mousemove'
                    },
                    series: [{
                        type: 'tree',
                        id: 0,
                        name: 'tree1',
                        data: [this.arr[i]],
                        top: '10%',
                        left: '8%',
                        bottom: '22%',
                        right: '20%',
                        symbolSize: 7,
                        edgeShape: 'polyline',
                        edgeForkPosition: '63%',
                        initialTreeDepth: 3,
                        lineStyle: {
                            width: 2
                        },
                        label: {
                            backgroundColor: '#fff',
                            position: 'left',
                            verticalAlign: 'middle',
                            align: 'right'
                        },
                        leaves: {
                            label: {
                                position: 'right',
                                verticalAlign: 'middle',
                                align: 'left'
                            }
                        },
                        emphasis: {
                            focus: 'descendant'
                        },
                        expandAndCollapse: true,
                        animationDuration: 550,
                        animationDurationUpdate: 750
                    }]
                });
            }
            // 基于准备好的dom，初始化echarts实例
            let myChart = this.$echarts.init(document.getElementById('myChart'))
            // 绘制图表
            const data = {
                name: 'vue',
                children: [{
                        name: '新建文件',
                    },
                    {
                        name: '组件传值',
                        src: 'www.baidu.com',
                        children: [{
                                name: '显示笔记',
                                value: 721
                            },
                            {
                                name: '新建笔记',
                                value: 721
                            }
                        ]
                    },
                    {
                        name: '生命周期',
                        children: [{
                                name: '显示笔记',
                                value: 8833
                            },
                            {
                                name: '新建笔记',
                                value: 1732
                            },
                            
                        ]
                    },
                ]
            };
            this.data = data;
            console.log(this.data);
            myChart.setOption({
                tooltip: {
                    trigger: 'item',
                    triggerOn: 'mousemove'
                },
                series: [{
                    type: 'tree',
                    id: 0,
                    name: 'tree1',
                    data: [data],
                    top: '10%',
                    left: '8%',
                    bottom: '22%',
                    right: '20%',
                    symbolSize: 7,
                    edgeShape: 'polyline',
                    edgeForkPosition: '63%',
                    initialTreeDepth: 3,
                    lineStyle: {
                        width: 2
                    },
                    label: {
                        backgroundColor: '#fff',
                        position: 'left',
                        verticalAlign: 'middle',
                        align: 'right'
                    },
                    leaves: {
                        label: {
                            position: 'right',
                            verticalAlign: 'middle',
                            align: 'left'
                        }
                    },
                    emphasis: {
                        focus: 'descendant'
                    },
                    expandAndCollapse: true,
                    animationDuration: 550,
                    animationDurationUpdate: 750
                }]
            });
            //   console.log(this.data);
            // console.log(this.series.data);
            let that = this;
            myChart.on('click', function (params) {
                that.now = params
                //    console.log(that.val);
                //    this.now.treeAncestors.push({name:that.val})
                 console.log(that.now);
                if (that.now.data.src != undefined) {
                    console.log(1);
                    // window.location.href="http://www.baidu.com"
                    // console.log(that.now.data.src);
                } else  {
                    console.log(1);
                    that.$message({
                        type: 'info',
                        message: `请新建笔记`});
                        }
                if(that.now.data.name == '显示笔记') {
                    if(that.$route.params.obj != null) {
                        that.now.data.src = that.$route.params.obj;
                        that.title = that.now.data.src.src[0].title;
                        that.context = that.now.data.src.src[0].context
                        console.log(that.title);
                    } 
                }
                if (that.now.data.name == '新建文件') {
                    // this.$router.go({name: 'edit', params: {name: that.now.data.name}});
                    that.open()
                    console.log(2);
                }
                if (that.now.data.name == '新建笔记') {
                    that.$router.push({name: 'edit', params: {
                        name: that.now.treeAncestors[2].name,
                        father: that.now.treeAncestors[1].name,
                        obj: that.now.data
                    }
                        });
                    //that.open()
                    console.log(2);
                }
            })
            myChart.setOption({
                tooltip: {
                    trigger: 'item',
                    triggerOn: 'mousemove'
                },
                series: [{
                    type: 'tree',
                    id: 0,
                    name: 'tree1',
                    data: [data],
                    top: '10%',
                    left: '8%',
                    bottom: '22%',
                    right: '20%',
                    symbolSize: 7,
                    edgeShape: 'polyline',
                    edgeForkPosition: '63%',
                    initialTreeDepth: 3,
                    lineStyle: {
                        width: 2
                    },
                    label: {
                        backgroundColor: '#fff',
                        position: 'left',
                        verticalAlign: 'middle',
                        align: 'right'
                    },
                    leaves: {
                        label: {
                            position: 'right',
                            verticalAlign: 'middle',
                            align: 'left'
                        }
                    },
                    emphasis: {
                        focus: 'descendant'
                    },
                    expandAndCollapse: true,
                    animationDuration: 550,
                    animationDurationUpdate: 750
                }]
            });
            this.myChart = myChart;
        },
    }
    }
</script>

<style>
#content {
    width: 300px;
    height: 35px;
    margin-top: 10px;
    border: 1px solid red;
    padding-left: 10px;
}
.title {
    z-index: 100;
    margin-top: 15%;
    margin-left: 40px;
}
.context {
    z-index: 100;
    margin-top: 10%;
    margin-left: 40px;
}
.box {
    width: 50%;
    height: 100%;
    border-left: 1px solid red;
    position: absolute;
    right: 0;
    top: 0;
    z-index: -10;
}
.pic_box {
    
}
</style>