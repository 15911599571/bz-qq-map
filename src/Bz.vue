<template>
  <div>
    <script-loader :scripts="scripts"></script-loader>
    <div id="map_container"></div>
  </div>
</template>

<script>
  import ScriptLoader from 'bz-script-loader'
  export default {
    props: {
      config_map: {
        default: null
      },
      value: {
        required: true
      }
    },
    components: {
      ScriptLoader
    },
    computed: {
    },
    data: function () {
      return {
        scripts: [
          '//map.qq.com/api/js?v=2.exp&callback=initMap'
        ],
        map: null
      }
    },
    mounted () {
      window.initMap = this.initMap
    },
    methods: {
      initMap: function () {
        this.map = new window.qq.maps.Map(
          document.getElementById('map_container'), {
            zoom: 12,
            zoomControl: false,
            // mapTypeId: window.qq.maps.MapTypeId.HYBRID, // ROADMAP, SATELLITE, HYBRID
            draggable: true,
            draggableCursor: 'crosshair',
            scrollwheel: true,
            disableDoubleClickZoom: true,
            mapTypeControl: false
          }
        )
        if (this.config_map) {
          this.config_map(this.map)
        }
        this.$emit('input', this.map)
      }
    }
  }
</script>
<style>
  #map_container {
    width: 100%;
    height: 100%;
  }
  /*屏蔽腾讯logo */
  div[style="position: absolute; left: 0px; top: 0px;"], // 左上角按钮
  div[style="position: absolute; z-index: 1000000; -webkit-user-select: none; left: 7px; bottom: 0px; "],
  div[style="position: absolute; z-index: 1000000; margin: 2px 5px 0px 2px; left: 0px; bottom: 0px; "],
  div[style="position: absolute; z-index: 1000000; -webkit-user-select: none; left: 7px; bottom: 0px;"],
  div[style="position: absolute; z-index: 1000000; margin: 2px 5px 0px 2px; left: 0px; bottom: 0px;"],
  div[style="position: absolute; z-index: 1000000; -webkit-user-select: none; left: 87px; bottom: 0px; "],
  div[style="position: absolute; z-index: 1000000; -webkit-user-select: none; left: 87px; bottom: 0px;"] {
    display: none;
  }
</style>
