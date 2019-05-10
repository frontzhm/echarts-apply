# echarts的简单运用

## TL;DR

* `<script src="https://cdn.bootcss.com/echarts/4.2.1/echarts.min.js"></script>`
* `var myEcharts = echarts.init(dom容器);var option = {};myChart.setOption(option)`
* option起码的选项，`{xAxis:{data:[]},yAxis:{},series:[{type:'line',data:[]}]}`
* 遇见困难[看文档](https://www.echartsjs.com/option.html#title)，没事敲敲[实例](https://echarts.baidu.com/examples/)快速增加对属性的理解
* [自己的玩的代码](https://github.com/frontzhm/echarts-apply)

<!-- more -->
## 下载

* [完整压缩版的地址](http://echarts.baidu.com/dist/echarts.min.js)
* [开发未压缩版的地址](http://echarts.baidu.com/dist/echarts.js)
* [cdn的地址](http://www.bootcdn.cn/echarts/)
* 急用测试的直接源码`<script src="https://cdn.bootcss.com/echarts/4.2.1/echarts.min.js"></script>`

## 先简单demo

* echarts的引入需要在head里
* 为echarts准备一个具备大小（宽高）的Dom
* 初始化echarts实例，`echarts.init(dom容器)`
* 实例设置配置项和数据，`myChart.setOption(option)`
* 重中之重的就是option了，[这里只是简单演示demo不做介绍](https://codepen.io/frontzhm/pen/KLpjxd)

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>ECharts</title>
    <!-- 引入 echarts.js -->
    <script src="https://cdn.bootcss.com/echarts/4.2.1/echarts.min.js"></script>
</head>
<body>
    <!-- 为ECharts准备一个具备大小（宽高）的Dom -->
    <div id="main" style="width: 600px;height:400px;"></div>
    <script type="text/javascript">
        // 基于准备好的dom，初始化echarts实例
        var myChart = echarts.init(document.getElementById('main'));

        // 指定图表的配置项和数据
        var option = {
            title: {
                text: 'ECharts 入门示例'
            },
            tooltip: {},
            legend: {
                data:['销量']
            },
            xAxis: {
                data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
            },
            yAxis: {},
            series: [{
                name: '销量',
                type: 'bar',
                data: [5, 20, 36, 10, 10, 20]
            }]
        };

        // 使用刚指定的配置项和数据显示图表。
        myChart.setOption(option);
    </script>
</body>
</html>
```

## option

想象小时候刚学条状图，一般会给班级的学生和成绩，然后在画出来。

这样，一般的步骤就：

* 先画个坐标系，横坐标纵坐标
* 然后横坐标画刻度线，一个刻度一个学生的名字
* 纵坐标也有刻度线，然后根据大家的成绩画出刻度线
* 最后根据学生的成绩画柱子

再看看echarts的option

* xAxis就是横坐标，里面的data就可以是学生名字，刻度默认会自动有
* yAxis就是纵坐标，注意里面的data，如果是数值，一般不用写，echarts已经计算好刻度了，超酷，如果不是可以再进行设置
* series可以画柱子，其是图的集合，里面可以画柱子图，折线图等等，这边设置`[{type:'bar',data:[各学生的分数]]}]`

### 延伸option

* 图例就是左上角那个是legend，配合series里面的name使用
* 鼠标hover每个柱子的提示框是tooltip
* series的`stack:'总量'`的时候，数据堆叠，同个类目轴上系列配置相同的stack值后，后一个系列的值会在前一个系列的值上相加。
* xAxis的`boundaryGap: false`坐标轴两边留白策略，类目轴和非类目轴的设置和表现不一样。刻度只是作为分隔线，标签和数据点都会在两个刻度之间的带(band)中间。
* 鼠标放在柱子上或者点上会显示提示框，里面有数据，`tooltip:{trigger:'axis'}`
* x轴上面的各个字段的控制是`label`
* 想要整体表格离容器有一定的边距，设置`grid`，这个控制就是表格占据的空间
* 想要右上角出现工具栏，像导出图片，编辑数据，`toolbox`
* 折线图占据的空间样式，比如背景色，就是`areaStyle`
* 右边也是y周的时候，`yAxis`是数组且标记右边的位置，对应的series如果以右边的话，`yAxisIndex:1`
* x轴太多数据，需要压缩图，就需要`dataZoom`，开始的视图显示`start end`，y视图自动变化`filterMode:filter`，一种滑块型，一种内置型
* series里面的data每一项可以是对象形式`{value:原本的值}`，这样可以有更多用处，比如和label的formatter配合使用

## 样式定义

* x轴的相关配置找[官网的文档](https://www.echartsjs.com/option.html#xAxis)，一般可能需要的刻度显示不一样啦，或者间距啦，一般默认x轴的都是名称之类的
* y轴的相关配置找[官网的文档](https://www.echartsjs.com/option.html#yAxis)，一般可能需要的刻度显示不一样啦，或者间距啦，一般简单的可以不写这个，因为y轴都是连续数据
* series的配置[官网的文档](https://www.echartsjs.com/option.html#series)，这里不同的图的配置去对应找不同的类型即可
