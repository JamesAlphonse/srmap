<template>
  <div>
    <div id="map-container" ref="mapContainer" @mousemove="onMouseMove">
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

    <svg width="500" height="500">
    <defs>
        <linearGradient id='stripe-gradient' x1='0%' y1='0%' x2='100%' y2='100%'>
            <stop offset='0%'  stop-color='red'></stop>
            <stop offset='12.45%'  stop-color='red'></stop>
            <stop offset='12.5%' stop-color='orange'></stop>
            <stop offset='24.45%' stop-color='orange'></stop>
            <stop offset='25.5%'  stop-color='red'></stop>
            <stop offset='37.45%'  stop-color='red'></stop>
            <stop offset='37.5%' stop-color='orange'></stop>
            <stop offset='49.9%' stop-color='orange'></stop>
            <stop offset='50%' stop-color='red'></stop>
            <stop offset='62.45%' stop-color='red'></stop>
            <stop offset='62.5%' stop-color='orange'></stop>
            <stop offset='74.95%' stop-color='orange'></stop>
            <stop offset='75%' stop-color='red'></stop>
            <stop offset='87.45%' stop-color='red'></stop>
            <stop offset='87.5%' stop-color='orange'></stop>
            <stop offset='100%' stop-color='orange'></stop>
        </linearGradient>
        <pattern id='stripe-pattern' width='20' height='20' patternUnits='userSpaceOnUse' >
            <rect x='-20' y='0' width='40' height='40' fill='url(#stripe-gradient)' stroke-width='0' stroke='none'>
                <animate attributeName='x' from='-20' to='0' dur='1s' repeatCount='indefinite'></animate>
            </rect>
        </pattern>
    </defs>
</svg>

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

  .war {
    fill: url(#stripe-pattern);
  }

  .lineRed {
    stroke:#FF0000;
    stroke-width: 20;
  }

  .lineOrange {
    stroke:#FF7700;
    stroke-width: 20;
    transform: translate(20px);
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
          container: this.$refs.mapContainer
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
          id: 'map',
        },
        info_data: {},
      }
    }
  }

</script>