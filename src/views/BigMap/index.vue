<template>
　 <div class="baidumap" id="allmap"></div>
</template>

<script>
import data from './custom_map_config.json'
export default {
    name: 'pm-distribution',
    components: {
    },
    mounted() {
        this.baiduMap()
        console.log(data);
    },
    methods: {
        baiduMap() {
            var map = new BMap.Map('allmap') // 创建地图实例
            map.setMapStyleV2({     
            styleId: '180596ae8c9763c8aa63d4baae7985b6'
            })
            var point = new BMap.Point(116.331398, 39.897445) // 创建点坐标
            map.centerAndZoom(point, 15) // 初始化地图，设置中心点坐标和地图级别
            map.enableScrollWheelZoom(true) //开启鼠标滚轮缩放

            map.addControl(new BMap.NavigationControl())
            map.addControl(new BMap.ScaleControl())
            map.addControl(new BMap.OverviewMapControl())
            map.addControl(new BMap.MapTypeControl())
            //map.setMapStyle({ style: 'midnight' }) //地图风格

            var marker = new window.BMap.Marker(point) // 创建标注
            map.addOverlay(marker) // 将标注添加到地图中

            //提示信息
            var infoWindow = new BMap.InfoWindow('这是提示信息')
            // 鼠标移上标注点要发生的事
            marker.addEventListener('mouseover', function() {
                this.openInfoWindow(infoWindow)
            })

            // 鼠标移开标注点要发生的事
            marker.addEventListener('mouseout', function() {
                //this.closeInfoWindow(infoWindow)
            })
        }
    }
}
</script>

<style lang="scss" scoped>
.baidumap {
    width: auto;
    height: auto;
    border: 1px solid red;
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    margin: auto;
}

.baidumap > .BMap_cpyCtrl {
    display: none !important;
}
.baidumap > .anchorBL {
    display: none !important;
}</style>
