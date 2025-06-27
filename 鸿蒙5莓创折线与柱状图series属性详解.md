大家好，欢迎回来鸿蒙5莓创图表组件的专场，我们这一期来讲解McLineBarChart组合图中最重要的series属性。series属性决定了图表中每个系列的表现形式和行为，是图表配置中最核心的部分。

## 1. show属性

作用：控制当前系列是否显示在图表中

类型：Boolean

默认值：true

可选值：

-   true：显示该系列
-   false：隐藏该系列

使用场景：当需要动态显示/隐藏某个数据系列时使用，比如在图表切换时。

```
series: [
  {
    name: '销售额',
    data: [1500, 1700, 1400, 2000, 1400, 1700, 1500],
    type: 'bar',
    show: false // 初始不显示该系列
  }
]
```

## 2. name属性

作用：定义系列名称，用于图例显示和tooltip提示

类型：String

默认值：无

使用场景：必须为每个系列设置名称，否则图例和提示信息无法正确显示。

```
series: [
  {
    name: '人流量', // 系列名称
    data: [1000, 1200, 900, 1500, 900, 1200, 1000],
    type: 'line'
  }
]
```

## 3. stack属性

作用：设置堆叠系列的名称，相同名称的系列会堆叠在一起

类型：String

默认值：无

使用场景：当需要展示多个系列的累计效果时使用，比如展示不同产品在总销售额中的贡献。

```
series: [
  {
    name: '产品A',
    data: [500, 700, 400, 600, 400, 700, 500],
    type: 'bar',
    stack: 'total' // 堆叠组名
  },
  {
    name: '产品B',
    data: [1000, 1000, 1000, 1400, 1000, 1000, 1000],
    type: 'bar',
    stack: 'total' // 与产品A堆叠在一起
  }
]
```

## 4. xAxisIndex属性

作用：指定系列使用的x轴索引

类型：Number

默认值：0

使用场景：当图表配置了多个x轴时，用于指定系列使用哪个x轴。

```
xAxis: [
  { data: ['Q1', 'Q2', 'Q3', 'Q4'] },
  { data: ['第一季度', '第二季度', '第三季度', '第四季度'] }
],
series: [
  {
    name: '销售额',
    data: [1500, 1700, 1400, 2000],
    type: 'bar',
    xAxisIndex: 1 // 使用第二个x轴
  }
]
```

## 5. yAxisIndex属性

作用：指定系列使用的y轴索引

类型：Number

默认值：0

使用场景：当图表配置了多个y轴时，用于指定系列使用哪个y轴，常用于双y轴图表。

```
yAxis: [
  { name: '销售额' },
  { name: '增长率', position: 'right' }
],
series: [
  {
    name: '销售额',
    data: [1500, 1700, 1400, 2000],
    type: 'bar'
  },
  {
    name: '增长率',
    data: [15, 17, 14, 20],
    type: 'line',
    yAxisIndex: 1 // 使用第二个y轴
  }
]
```

## 6. data属性

作用：设置系列的数据值

类型：Array<String|Number|Object>

默认值：[]

使用场景：必须为每个系列设置数据，支持三种格式：

-   纯数值数组：[100, 200, 300]
-   字符串数组：['100', '200', '300']
-   对象数组（仅bar类型支持）：[{value: 100, color: '#ff0000'}]

```
series: [
  {
    name: '销售额',
    data: [1500, 1700, 1400, 2000], // 纯数值
    type: 'bar'
  },
  {
    name: '特殊值',
    data: [
      {value: 1000, color: '#ff0000'}, // 红色柱子
      {value: 1200, color: '#00ff00'}, // 绿色柱子
      900, // 默认颜色柱子
      1500
    ],
    type: 'bar'
  }
]
```

## 7. label属性

作用：配置系列上显示的文本标签

类型：Object

默认值：{}

子属性：

-   show：是否显示标签（Boolean，默认false）
-   position：标签位置（String，默认'top'）
-   color：标签颜色（String，默认'#000'）
-   fontSize：字体大小（Number，默认12）
-   fontWeight：字体粗细（String，默认'normal'）
-   formatter：标签内容格式化函数（Function）

使用场景：当需要在图表上直接显示数值时使用。

```
series: [
  {
    name: '销售额',
    data: [1500, 1700, 1400, 2000],
    type: 'bar',
    label: {
      show: true,
      position: 'inside', // 标签显示在柱子内部
      color: '#fff',
      fontSize: 14,
      fontWeight: 'bold',
      formatter: (value) => `¥${value}`
    }
  }
]
```

## 8. rLevel属性

作用：设置系列渲染层级

类型：Number

默认值：0

使用场景：当需要控制多个系列的显示层级时使用，数值越大显示在越上层。

```
series: [
  {
    name: '背景',
    data: [2000, 2000, 2000, 2000],
    type: 'bar',
    rLevel: 0 // 底层
  },
  {
    name: '销售额',
    data: [1500, 1700, 1400, 2000],
    type: 'bar',
    rLevel: 1 // 上层
  }
]
```

## 9. animationCurve属性

作用：设置系列动画的缓动效果

类型：String

默认值：'easeOutCubic'

可选值：'linear', 'easeInQuad', 'easeOutQuad', 'easeInOutQuad', 'easeInCubic', 'easeOutCubic', 'easeInOutCubic', 'easeInQuart', 'easeOutQuart', 'easeInOutQuart', 'easeInQuint', 'easeOutQuint', 'easeInOutQuint', 'easeInSine', 'easeOutSine', 'easeInOutSine', 'easeInExpo', 'easeOutExpo', 'easeInOutExpo', 'easeInCirc', 'easeOutCirc', 'easeInOutCirc', 'easeInBack', 'easeOutBack', 'easeInOutBack', 'easeInElastic', 'easeOutElastic', 'easeInOutElastic', 'easeInBounce', 'easeOutBounce', 'easeInOutBounce'

使用场景：当需要自定义系列动画效果时使用。

```
series: [
  {
    name: '销售额',
    data: [1500, 1700, 1400, 2000],
    type: 'bar',
    animationCurve: 'easeOutBounce' // 弹跳动画效果
  }
]
```

## 10. animationFrame属性

作用：设置系列动画的帧数

类型：Number

默认值：30

使用场景：当需要调整动画流畅度或性能时使用。

```
series: [
  {
    name: '销售额',
    data: [1500, 1700, 1400, 2000],
    type: 'bar',
    animationFrame: 60 // 更流畅的动画
  }
]
```

## 11. smooth属性

作用：是否显示为平滑曲线

类型：Boolean

默认值：false

可选值：

-   true：平滑曲线
-   false：折线

使用场景：当需要展示更柔和的趋势线时使用。

```
series: [
  {
    name: '趋势线',
    data: [1500, 1700, 1400, 2000],
    type: 'line',
    smooth: true // 平滑曲线
  }
]
```

## 12. lineStyle属性

作用：配置线条样式（仅对line类型有效）

类型：Object

默认值：{}

子属性：

-   color：线条颜色（String，默认系列颜色）
-   width：线条宽度（Number，默认2）
-   type：线条类型（String，默认'solid'）
-   dash：虚线配置（Array，无默认值）
-   cap：线条端点样式（String，默认'butt'）

使用场景：当需要自定义线条外观时使用。

```
series: [
  {
    name: '趋势线',
    data: [1500, 1700, 1400, 2000],
    type: 'line',
    lineStyle: {
      color: '#ff0000',
      width: 4,
      type: 'dashed', // 虚线
      dash: [10, 5], // 虚线样式
      cap: 'round' // 圆角端点
    }
  }
]
```

## 13. itemStyle属性

作用：配置系列中每个数据点的样式

类型：Object

默认值：{}

子属性：

-   color：数据点颜色（String，默认系列颜色）
-   borderColor：边框颜色（String，默认'#fff'）
-   borderWidth：边框宽度（Number，默认1）
-   radius：圆角半径（Number，默认0）
-   shadowBlur：阴影模糊大小（Number，默认0）
-   shadowColor：阴影颜色（String，默认'rgba(0,0,0,0.5)'）
-   shadowOffsetX：阴影X偏移（Number，默认0）
-   shadowOffsetY：阴影Y偏移（Number，默认0）

使用场景：当需要自定义数据点外观时使用。

```
series: [
  {
    name: '数据点',
    data: [1500, 1700, 1400, 2000],
    type: 'line',
    itemStyle: {
      color: '#37a2da',
      borderColor: '#fff',
      borderWidth: 2,
      radius: 10, // 圆形数据点
      shadowBlur: 10,
      shadowColor: 'rgba(0,0,0,0.3)'
    }
  }
]
```

## 14. areaStyle属性

作用：配置区域填充样式（仅对line类型有效）

类型：Object

默认值：{}

子属性：

-   show：是否显示区域填充（Boolean，默认false）
-   color：填充颜色（String|Array|Object，默认系列颜色）
-   origin：填充起始位置（String，默认'auto'）
-   opacity：填充透明度（Number，默认1）

使用场景：当需要展示面积图效果时使用。

```
series: [
  {
    name: '面积图',
    data: [1500, 1700, 1400, 2000],
    type: 'line',
    areaStyle: {
      show: true,
      color: {
        type: 'linear',
        x: 0,
        y: 0,
        x2: 0,
        y2: 1,
        colorStops: [{
          offset: 0,
          color: 'rgba(55,162,218,0.8)'
        }, {
          offset: 1,
          color: 'rgba(55,162,218,0.1)'
        }]
      },
      origin: 'start', // 从y轴0开始填充
      opacity: 0.8
    }
  }
]
```

## 15. endLabel属性

作用：配置系列末端的标签

类型：Object

默认值：{}

子属性：

-   show：是否显示末端标签（Boolean，默认false）
-   value：自定义显示值（String|Number，默认数据值）
-   color：标签颜色（String，默认系列颜色）
-   fontSize：字体大小（Number，默认12）
-   fontWeight：字体粗细（String，默认'normal'）
-   offset：标签偏移量（Array，默认[0, 0]）

使用场景：当需要突出显示系列最后一个数据点时使用。

```
series: [
  {
    name: '趋势',
    data: [1500, 1700, 1400, 2000],
    type: 'line',
    endLabel: {
      show: true,
      value: '当前值',
      color: '#ff0000',
      fontSize: 16,
      fontWeight: 'bold',
      offset: [10, 0] // 向右偏移10px
    }
  }
]
```

## 16. shapeType属性

作用：设置柱状图形状类型（仅对bar类型有效）

类型：String

默认值：'normal'

可选值：

-   'normal'：普通柱状图
-   'leftEchelon'：左阶梯状柱状图
-   'rightEchelon'：右阶梯状柱状图

使用场景：当需要创建特殊形状的柱状图时使用。

```
series: [
  {
    name: '阶梯状',
    data: [1500, 1700, 1400, 2000],
    type: 'bar',
    shapeType: 'leftEchelon' // 左阶梯状
  }
]
```

## 17. echelonOffset属性

作用：设置阶梯状柱状图的锐度偏移量（仅对bar类型有效）

类型：Number

默认值：10

使用场景：当使用shapeType为leftEchelon或rightEchelon时，用于控制阶梯的锐度。

```
series: [
  {
    name: '阶梯状',
    data: [1500, 1700, 1400, 2000],
    type: 'bar',
    shapeType: 'leftEchelon',
    echelonOffset: 20 // 更大的偏移量
  }
]
```

## 18. backgroundStyle属性

作用：配置背景柱状图样式（仅对bar类型有效）

类型：Object

默认值：{}

子属性：

-   show：是否显示背景（Boolean，默认false）
-   color：背景颜色（String，默认'#f6f6f6'）
-   width：背景宽度（Number，默认柱状图宽度）
-   radius：背景圆角（Number，默认0）

使用场景：当需要为柱状图添加背景参考时使用。

```
series: [
  {
    name: '销售额',
    data: [1500, 1700, 1400, 2000],
    type: 'bar',
    backgroundStyle: {
      show: true,
      color: '#f0f0f0',
      width: '80%', // 比柱子宽
      radius: 4 // 圆角背景
    }
  }
]
```

## 19. gradient属性

作用：配置渐变色（仅对bar类型有效）

类型：Object

默认值：{}

子属性：

-   color：渐变色数组（Array，默认[]）
-   direction：渐变方向（String，默认'vertical'）

使用场景：当需要为柱状图添加渐变效果时使用。

```
series: [
  {
    name: '渐变柱',
    data: [1500, 1700, 1400, 2000],
    type: 'bar',
    gradient: {
      color: ['#37a2da', '#67e0e3'], // 蓝到青的渐变
      direction: 'horizontal' // 水平渐变
    }
  }
]
```

## 20. barStyle属性

作用：配置柱状图样式（仅对bar类型有效）

类型：Object

默认值：{}

子属性：

-   stroke：描边颜色（String，默认无描边）
-   strokeWidth：描边宽度（Number，默认1）
-   radius：柱状图圆角（Number|Array，默认0）
-   shadow：阴影配置（Object，默认无阴影）

使用场景：当需要自定义柱状图外观时使用。

```
series: [
  {
    name: '圆角柱',
    data: [1500, 1700, 1400, 2000],
    type: 'bar',
    barStyle: {
      stroke: '#333',
      strokeWidth: 2,
      radius: [10, 10, 0, 0], // 仅顶部圆角
      shadow: {
        color: 'rgba(0,0,0,0.3)',
        blur: 10,
        offsetX: 0,
        offsetY: 5
      }
    }
  }
]
```

## 实际应用案例

下面是一个综合使用多个series属性的实际案例，展示了一个销售仪表板：

```
@Entry
@Component
struct SalesDashboard {
  @State options: Options = new Options({
    title: {
      show: true,
      text: '销售仪表板',
      right: 20,
      top: 22
    },
    legend: {
      show: true,
      bottom: 10
    },
    xAxis: {
      data: ['1月', '2月', '3月', '4月', '5月', '6月']
    },
    yAxis: [
      { name: '销售额(万)' },
      { 
        name: '增长率(%)',
        position: 'right',
        splitLine: { show: false }
      }
    ],
    series: [
      {
        name: '目标',
        data: [120, 120, 120, 120, 120, 120],
        type: 'bar',
        backgroundStyle: {
          show: true,
          color: '#f6f6f6'
        },
        barStyle: {
          radius: 0
        },
        rLevel: 0
      },
      {
        name: '销售额',
        data: [100, 130, 110, 150, 140, 160],
        type: 'bar',
        gradient: {
          color: ['#37a2da', '#67e0e3']
        },
        barStyle: {
          radius: [5, 5, 0, 0]
        },
        label: {
          show: true,
          position: 'top',
          color: '#333'
        },
        rLevel: 1
      },
      {
        name: '增长率',
        data: [10, 30, 10, 50, 40, 60],
        type: 'line',
        yAxisIndex: 1,
        smooth: true,
        lineStyle: {
          width: 3
        },
        itemStyle: {
          color: '#ff0000',
          radius: 5
        },
        areaStyle: {
          show: true,
          color: 'rgba(255,0,0,0.1)'
        },
        endLabel: {
          show: true,
          value: '当前增长率',
          color: '#ff0000',
          fontSize: 14
        }
      }
    ]
  });

  build() {
    Row() {
      McLineBarChart({ options: this.options })
    }
    .height('50%')
  }
}
```

这个案例中：

1.  使用背景柱状图展示销售目标
1.  使用渐变柱状图展示实际销售额
1.  使用平滑曲线和面积图展示增长率
1.  添加了末端标签突出当前增长率
1.  通过rLevel控制系列层级

好，这期讲到这里就结束了，希望大家通过这篇文章能够全面掌握McLineBarChart的series属性配置，在实际项目中灵活运用这些属性创建出精美的组合图表。如果有任何问题，欢迎在评论区留言讨论。