Hello everyone, welcome back to the special session on HarmonyOS 5 Meichuang chart components. In this episode, we'll explain the most important `series` property in the McLineBarChart combined chart. The `series` property determines the presentation form and behavior of each series in the chart, serving as the core part of chart configuration.  


## 1. `show` Property  
**Function**: Controls whether the current series is displayed in the chart.  
**Type**: Boolean  
**Default**: `true`  
**Options**:  
- `true`: Display the series.  
- `false`: Hide the series.  
**Usage Scenario**: Use when dynamically showing/hiding a data series, such as during chart switching.  

```typescript
series: [
  {
    name: 'Sales',
    data: [1500, 1700, 1400, 2000, 1400, 1700, 1500],
    type: 'bar',
    show: false // Do not display this series initially
  }
]
```  


## 2. `name` Property  
**Function**: Defines the series name for legend display and tooltip hints.  
**Type**: String  
**Default**: None  
**Usage Scenario**: Must set a name for each series; otherwise, legend and tooltip information cannot be displayed correctly.  

```typescript
series: [
  {
    name: 'Foot Traffic', // Series name
    data: [1000, 1200, 900, 1500, 900, 1200, 1000],
    type: 'line'
  }
]
```  


## 3. `stack` Property  
**Function**: Sets the name of the stacked series; series with the same name will be stacked together.  
**Type**: String  
**Default**: None  
**Usage Scenario**: Use when showing the cumulative effect of multiple series, such as demonstrating the contribution of different products to total sales.  

```typescript
series: [
  {
    name: 'Product A',
    data: [500, 700, 400, 600, 400, 700, 500],
    type: 'bar',
    stack: 'total' // Stack group name
  },
  {
    name: 'Product B',
    data: [1000, 1000, 1000, 1400, 1000, 1000, 1000],
    type: 'bar',
    stack: 'total' // Stacked with Product A
  }
]
```  


## 4. `xAxisIndex` Property  
**Function**: Specifies the x-axis index used by the series.  
**Type**: Number  
**Default**: `0`  
**Usage Scenario**: When the chart configures multiple x-axes, specify which x-axis the series uses.  

```typescript
xAxis: [
  { data: ['Q1', 'Q2', 'Q3', 'Q4'] },
  { data: ['1st Qtr', '2nd Qtr', '3rd Qtr', '4th Qtr'] }
],
series: [
  {
    name: 'Sales',
    data: [1500, 1700, 1400, 2000],
    type: 'bar',
    xAxisIndex: 1 // Use the second x-axis
  }
]
```  


## 5. `yAxisIndex` Property  
**Function**: Specifies the y-axis index used by the series.  
**Type**: Number  
**Default**: `0`  
**Usage Scenario**: When the chart configures multiple y-axes, specify which y-axis the series uses, commonly used in dual y-axis charts.  

```typescript
yAxis: [
  { name: 'Sales' },
  { name: 'Growth Rate', position: 'right' }
],
series: [
  {
    name: 'Sales',
    data: [1500, 1700, 1400, 2000],
    type: 'bar'
  },
  {
    name: 'Growth Rate',
    data: [15, 17, 14, 20],
    type: 'line',
    yAxisIndex: 1 // Use the second y-axis
  }
]
```  


## 6. `data` Property  
**Function**: Sets the data values of the series.  
**Type**: Array<String|Number|Object>  
**Default**: `[]`  
**Usage Scenario**: Must set data for each series, supporting three formats:  
- Pure numeric array: `[100, 200, 300]`  
- String array: `['100', '200', '300']`  
- Object array (only supported by bar type): `[{value: 100, color: '#ff0000'}]`  

```typescript
series: [
  {
    name: 'Sales',
    data: [1500, 1700, 1400, 2000], // Pure numeric
    type: 'bar'
  },
  {
    name: 'Special Values',
    data: [
      {value: 1000, color: '#ff0000'}, // Red column
      {value: 1200, color: '#00ff00'}, // Green column
      900, // Default color column
      1500
    ],
    type: 'bar'
  }
]
```  


## 7. `label` Property  
**Function**: Configures text labels displayed on the series.  
**Type**: Object  
**Default**: `{}`  
**Sub-properties**:  
- `show`: Whether to display labels (Boolean, default `false`).  
- `position`: Label position (String, default `'top'`).  
- `color`: Label color (String, default `'#000'`).  
- `fontSize`: Font size (Number, default `12`).  
- `fontWeight`: Font weight (String, default `'normal'`).  
- `formatter`: Label content formatting function (Function).  
**Usage Scenario**: Use when directly displaying values on the chart.  

```typescript
series: [
  {
    name: 'Sales',
    data: [1500, 1700, 1400, 2000],
    type: 'bar',
    label: {
      show: true,
      position: 'inside', // Labels inside the column
      color: '#fff',
      fontSize: 14,
      fontWeight: 'bold',
      formatter: (value) => `¥${value}`
    }
  }
]
```  


## 8. `rLevel` Property  
**Function**: Sets the series rendering level.  
**Type**: Number  
**Default**: `0`  
**Usage Scenario**: Use when controlling the display hierarchy of multiple series; larger values are displayed on top.  

```typescript
series: [
  {
    name: 'Background',
    data: [2000, 2000, 2000, 2000],
    type: 'bar',
    rLevel: 0 // Bottom layer
  },
  {
    name: 'Sales',
    data: [1500, 1700, 1400, 2000],
    type: 'bar',
    rLevel: 1 // Top layer
  }
]
```  


## 9. `animationCurve` Property  
**Function**: Sets the easing effect of series animation.  
**Type**: String  
**Default**: `'easeOutCubic'`  
**Options**: `'linear'`, `'easeInQuad'`, `'easeOutQuad'`, `'easeInOutQuad'`, `'easeInCubic'`, `'easeOutCubic'`, `'easeInOutCubic'`, `'easeInQuart'`, `'easeOutQuart'`, `'easeInOutQuart'`, `'easeInQuint'`, `'easeOutQuint'`, `'easeInOutQuint'`, `'easeInSine'`, `'easeOutSine'`, `'easeInOutSine'`, `'easeInExpo'`, `'easeOutExpo'`, `'easeInOutExpo'`, `'easeInCirc'`, `'easeOutCirc'`, `'easeInOutCirc'`, `'easeInBack'`, `'easeOutBack'`, `'easeInOutBack'`, `'easeInElastic'`, `'easeOutElastic'`, `'easeInOutElastic'`, `'easeInBounce'`, `'easeOutBounce'`, `'easeInOutBounce'`.  
**Usage Scenario**: Use when customizing series animation effects.  

```typescript
series: [
  {
    name: 'Sales',
    data: [1500, 1700, 1400, 2000],
    type: 'bar',
    animationCurve: 'easeOutBounce' // Bounce animation effect
  }
]
```  


## 10. `animationFrame` Property  
**Function**: Sets the frame rate of series animation.  
**Type**: Number  
**Default**: `30`  
**Usage Scenario**: Use when adjusting animation smoothness or performance.  

```typescript
series: [
  {
    name: 'Sales',
    data: [1500, 1700, 1400, 2000],
    type: 'bar',
    animationFrame: 60 // Smoother animation
  }
]
```  


## 11. `smooth` Property  
**Function**: Whether to display as a smooth curve.  
**Type**: Boolean  
**Default**: `false`  
**Options**:  
- `true`: Smooth curve.  
- `false`: Polyline.  
**Usage Scenario**: Use when showing a softer trend line.  

```typescript
series: [
  {
    name: 'Trend Line',
    data: [1500, 1700, 1400, 2000],
    type: 'line',
    smooth: true // Smooth curve
  }
]
```  


## 12. `lineStyle` Property  
**Function**: Configures line styles (only valid for line type).  
**Type**: Object  
**Default**: `{}`  
**Sub-properties**:  
- `color`: Line color (String, default series color).  
- `width`: Line width (Number, default `2`).  
- `type`: Line type (String, default `'solid'`).  
- `dash`: Dashed line configuration (Array, no default).  
- `cap`: Line end style (String, default `'butt'`).  
**Usage Scenario**: Use when customizing line appearance.  

```typescript
series: [
  {
    name: 'Trend Line',
    data: [1500, 1700, 1400, 2000],
    type: 'line',
    lineStyle: {
      color: '#ff0000',
      width: 4,
      type: 'dashed', // Dashed line
      dash: [10, 5], // Dashed pattern
      cap: 'round' // Rounded ends
    }
  }
]
```  


## 13. `itemStyle` Property  
**Function**: Configures the style of each data point in the series.  
**Type**: Object  
**Default**: `{}`  
**Sub-properties**:  
- `color`: Data point color (String, default series color).  
- `borderColor`: Border color (String, default `'#fff'`).  
- `borderWidth`: Border width (Number, default `1`).  
- `radius`: Corner radius (Number, default `0`).  
- `shadowBlur`: Shadow blur size (Number, default `0`).  
- `shadowColor`: Shadow color (String, default `'rgba(0,0,0,0.5)'`).  
- `shadowOffsetX`: Shadow X offset (Number, default `0`).  
- `shadowOffsetY`: Shadow Y offset (Number, default `0`).  
**Usage Scenario**: Use when customizing data point appearance.  

```typescript
series: [
  {
    name: 'Data Points',
    data: [1500, 1700, 1400, 2000],
    type: 'line',
    itemStyle: {
      color: '#37a2da',
      borderColor: '#fff',
      borderWidth: 2,
      radius: 10, // Circular data points
      shadowBlur: 10,
      shadowColor: 'rgba(0,0,0,0.3)'
    }
  }
]
```  


## 14. `areaStyle` Property  
**Function**: Configures area fill styles (only valid for line type).  
**Type**: Object  
**Default**: `{}`  
**Sub-properties**:  
- `show`: Whether to show area fill (Boolean, default `false`).  
- `color`: Fill color (String|Array|Object, default series color).  
- `origin`: Fill start position (String, default `'auto'`).  
- `opacity`: Fill transparency (Number, default `1`).  
**Usage Scenario**: Use when showing area chart effects.  

```typescript
series: [
  {
    name: 'Area Chart',
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
      origin: 'start', // Fill from y-axis 0
      opacity: 0.8
    }
  }
]
```  


## 15. `endLabel` Property  
**Function**: Configures the label at the end of the series.  
**Type**: Object  
**Default**: `{}`  
**Sub-properties**:  
- `show`: Whether to show the end label (Boolean, default `false`).  
- `value`: Custom display value (String|Number, default data value).  
- `color`: Label color (String, default series color).  
- `fontSize`: Font size (Number, default `12`).  
- `fontWeight`: Font weight (String, default `'normal'`).  
- `offset`: Label offset (Array, default `[0, 0]`).  
**Usage Scenario**: Use when highlighting the last data point of the series.  

```typescript
series: [
  {
    name: 'Trend',
    data: [1500, 1700, 1400, 2000],
    type: 'line',
    endLabel: {
      show: true,
      value: 'Current Value',
      color: '#ff0000',
      fontSize: 16,
      fontWeight: 'bold',
      offset: [10, 0] // Offset 10px to the right
    }
  }
]
```  


## 16. `shapeType` Property  
**Function**: Sets the bar chart shape type (only valid for bar type).  
**Type**: String  
**Default**: `'normal'`  
**Options**:  
- `'normal'`: Normal bar chart.  
- `'leftEchelon'`: Left echelon bar chart.  
- `'rightEchelon'`: Right echelon bar chart.  
**Usage Scenario**: Use when creating bar charts with special shapes.  

```typescript
series: [
  {
    name: 'Echelon',
    data: [1500, 1700, 1400, 2000],
    type: 'bar',
    shapeType: 'leftEchelon' // Left echelon shape
  }
]
```  


## 17. `echelonOffset` Property  
**Function**: Sets the sharpness offset of echelon bar charts (only valid for bar type).  
**Type**: Number  
**Default**: `10`  
**Usage Scenario**: When `shapeType` is `leftEchelon` or `rightEchelon`, control the sharpness of the echelon.  

```typescript
series: [
  {
    name: 'Echelon',
    data: [1500, 1700, 1400, 2000],
    type: 'bar',
    shapeType: 'leftEchelon',
    echelonOffset: 20 // Larger offset
  }
]
```  


## 18. `backgroundStyle` Property  
**Function**: Configures the background bar chart style (only valid for bar type).  
**
