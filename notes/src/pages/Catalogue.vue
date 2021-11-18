<template>
    <div id="catelogue">
        <div id="myChart" :style="{width: '500px', height: '800px'}"></div>
        <div v-for="(item,index) in arr" :key="index" :id="item.id" :style="{width: '500px', height: '800px'}">
            {{item}}
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Catelogue',
        mounted() {
            this.drawLine();
        },
        data() {
            return {
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
                    window.location.href="http://www.baidu.com"
                }
                if (that.now.data.name == '新建文件') {
                    // this.$router.go({name: 'edit', params: {name: that.now.data.name}});
                    that.open()
                    console.log(2);
                }
                if (that.now.data.name == '新建笔记') {
                    that.$router.push({name: 'edit', params: {
                        name: that.now.treeAncestors[2].name,
                        father: that.now.treeAncestors[0].name,
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
</style>