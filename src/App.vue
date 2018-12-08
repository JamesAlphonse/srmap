<template>
  <div>
    <div id="map-container" @mousemove="onMouseMove">
      <simple-svg
        :filepath="map.filepath"
        :fill="map.fill"
        :stroke="map.stroke"
        :width="map.width"
        :height="map.height"
        :id="map.id"
      />
    </div>

    <InfoContainer :package="info_data"/>
  </div>
</template>

<style lang="scss">
  body {
    padding: 0; margin: 0;
  }

  #map-container {
    position: relative;
    display: block;
    margin: 0px auto;
    background: grey;
  }

  .state {
    fill: #B0B0B0;
    transition: all 0.2s;
  }

  .active {
    fill: #89baf6;
  }

  .active:hover {
    fill: #1547D1;
  }
</style>

<script>
  import {SimpleSVG} from 'vue-simple-svg'
  import InfoContainer from '@/components/InfoContainer'

  export default {
    name: 'App',
    components: {
      'simple-svg': SimpleSVG,
      InfoContainer
    },
    mounted() {
    },
    methods: {
      onMouseMove(e) {
        this.info_data = {
          x: e.pageX,
          y: e.pageY,
          id: e.target.id,
          class: e.target.className.baseVal,
        }
      }
    },
    data() {
      return {
        map: {
          filepath: '/static/map.svg',
          fill: '#d2d2d2',
          stroke: '',
          width: '100%',
          height: '100%',
          id: 'map'
        },
        info_data: {},
      }
    }
  }

</script>