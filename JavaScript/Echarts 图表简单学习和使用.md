# Echarts 图表简单学习和使用

#### 使用例子 TODO

```javascript
import echarts from 'echarts';

const echart = echarts.init(dom);

TODO

```

#### 学习路径

echarts 是 apache 顶级项目（孵化中 18年开始）

官方文档非常优秀，尤其是中文文档，原因是 echarts 是源自 baidu。

[Echarts 官方文档](https://echarts.apache.org/zh/index.html)

echarts learning

- 概念：instant + series + component
- 执行：
    dom(渲染后) 
    \+ echart = echarts.init(dom) 
    \+ optioon = {...component + series} 
    \+ echart.setOption(option)
- 数据：
    series.data 和 option.dataset
- 组件定位：遵循css，以初始化dom为界，辅以绝对位置。
- 坐标系：
    直角坐标 + 日历坐标
- 个性化 & 样式：
    主题（js 引入，echarts.init）+ 调色盘（option）+ 直接设置样式（itemStyle，lineStyle...）+ 高亮（鼠标悬浮，option.emphasis）
- 异步加载：
    setOption（数据 series.name 对应）, loading（echart.showLoading()/hideLoading()）
- 数据集 dataset：
    可被多个组件复用, dimensions 纬度, dataset=》series， 数据到图形映射（series.encode），
    dimensions：列/表 + 数据项（dataitem）
- 图表交互组件：
      图例-legend，标题-title，视觉映射-visualMap，缩放-dataZoom，时间线-timeline
- 数据视觉映射 visualMap：
    类别（symbol），大小（symbolSize），颜色（color），透明度（opacity），颜色透明度（colorAlpha），明暗（colorLightness），饱和度（colorSaturation），色调（colorHue）
- 日历组件：
    calender
