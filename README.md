# China GeoJSON

最新中国地图 GeoJSON 数据，支持省级、市级边界绘制。适用于 D3.js、ECharts、Mapbox 等地图可视化库。

🌐 **在线演示**: https://yezongyang.github.io/china-map/

## 📊 数据概览

| 数据层级 | 文件数 | 说明 |
|---------|-------|------|
| 全国 | 1 | `china.json` 完整中国地图 |
| 省级 | 34 | 各省/直辖市/自治区/特别行政区 |
| 市级 | 344 | 各地级市/地区/自治州 |

## 📁 文件结构

```
china-geojson/
├── china.json              # 全国 GeoJSON
├── geometryProvince/       # 省级 GeoJSON
│   ├── 11.json            # 北京市
│   ├── 12.json            # 天津市
│   ├── 13.json            # 河北省
│   └── ...                # 共34个
├── geometryCouties/        # 市级 GeoJSON
│   ├── 1101.json          # 北京市辖区
│   ├── 1301.json          # 石家庄市
│   └── ...                # 共344个
└── README.md
```

## 🗺️ 行政区划代码

采用国家统计局 6 位行政区划代码：

| 代码 | 地区 |
|------|------|
| 11 | 北京市 |
| 31 | 上海市 |
| 44 | 广东省 |
| 33 | 浙江省 |
| ... | ... |

> 完整代码对照表参考 [国家统计局](https://www.stats.gov.cn/tjsj/tjbz/tjyqhdmhcxhfdm/)

## 💡 使用示例

### D3.js

```javascript
// 加载全国地图
d3.json('china.json').then(function(geojson) {
  svg.append('g')
    .selectAll('path')
    .data(geojson.features)
    .enter()
    .append('path')
    .attr('d', d3.geoPath())
    .attr('fill', '#69b3a2');
});

// 加载某省地图
d3.json('geometryProvince/44.json').then(...) // 广东省
```

### ECharts

```javascript
// 注册地图
echarts.registerMap('china', chinaJson);

// 使用
option = {
  series: [{
    type: 'map',
    map: 'china',
    data: [
      {name: '北京', value: 100},
      {name: '上海', value: 200}
    ]
  }]
};
```

### Mapbox / Leaflet

```javascript
// 添加 GeoJSON 图层
map.addSource('china', {
  type: 'geojson',
  data: 'china.json'
});

map.addLayer({
  id: 'china-fill',
  source: 'china',
  type: 'fill',
  paint: {
    'fill-color': '#088',
    'fill-opacity': 0.5
  }
});
```

## 🔧 数据说明

- **坐标系**: WGS84 (EPSG:4326)
- **数据精度**: 适合省级、市级展示
- **更新频率**: 跟随行政区划调整更新
- **文件大小**: 全国数据约 54KB

## 📦 快速开始

### 1. 克隆仓库

```bash
git clone https://github.com/Rockelbel/china-geojson.git
```

### 2. 引入数据

```html
<!-- 直接引用 -->
<script src="china-geojson/china.json"></script>
```

或

```javascript
// 打包引入
import chinaJson from 'china-geojson/china.json';
```

### 3. 绘制地图

参考上方 [使用示例](#-使用示例)

## 🌟 特性

- ✅ 标准 GeoJSON 格式
- ✅ 完整省级数据（34个）
- ✅ 详细市级数据（344个）
- ✅ 支持 D3.js、ECharts、Mapbox
- ✅ 支持数据绑定与交互

## 📝 更新记录

| 日期 | 更新内容 |
|------|---------|
| 2020-01 | 初始版本，包含全国及省级数据 |
| 2020-07 | 补充市级数据 |

## 🤝 贡献

数据来源于公开渠道，如发现行政区划变更未及时更新，欢迎提交 PR。

## 📄 许可证

MIT License

## 🔗 相关链接

- [国家统计局行政区划代码](https://www.stats.gov.cn/tjsj/tjbz/tjyqhdmhcxhfdm/)
- [D3.js 地理投影](https://d3js.org/d3-geo)
- [ECharts 地图](https://echarts.apache.org/zh/option.html#series-map)

---

**注意**: 本数据仅供开发测试使用，如需精确地理数据请使用官方测绘资料。
