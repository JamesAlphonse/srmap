<template>
    <!--
      :style="{transform: `translate3d(${point.x}px,${point.y}px,-1px)`, opacity: display}"
    -->
    <div id="info-container" ref="info"
      :style="{
        transform: `translate3d(${point.x}px,${point.y}px,-1px)`,
        opacity: opacity
      }"
    >
      {{ state.name }}
    </div>
</template>

<style lang="scss" scoped>
  #info-container {
    position: absolute;
    display: block;
    padding: 15px;
    text-align: center;
    top: 0;
    left: 0;
    transform: translate(0, 0);
    border: 1px solid #fff;
    background: rgba(0,0,0,0.8);
    transition: transform 0.07s, opacity 0.2s, content 2s;
    will-change: transform;
    color: #fff;
    pointer-events: none;
    box-shadow: 0px 0px 10px 1px #ccc;
    opacity: 0;
    z-index: 999;
  }
</style>

<script>
  import jsonRaw from '@/data/states.json'

  export default {
    name: 'InfoContainer',
    props: ['package'],
    components: {
    },
    mounted() {
    },
    watch: {
      package: function() {
        if(this.package.class == 'state active' && this.package.id.length == 2){
          if(this.package.x < this.threshold)
            this.offset.x = 50
          else if(this.package.x > this.package.container.clientWidth - this.threshold)
            this.offset.x = -50 - this.$refs.info.clientWidth

          if(this.package.y < this.threshold)
            this.offset.y = 50
          else if(this.package.y > this.package.container.clientHeight - this.threshold)
            this.offset.y = -50 - this.$refs.info.clientHeight

          this.point.x = this.package.x + this.offset.x
          this.point.y = this.package.y + this.offset.y
          
          this.opacity = 1

          if(this.json[this.package.id])
            this.state.name = this.json[this.package.id].name 
        }
        else{
          this.opacity = 0
          this.state.name = ''
        }
      }
    },
    methods: {
    },
    data() {
      return {
        json: jsonRaw,
        state: {
          name: ''
        },
        point: {
          x: 0,
          y: 0
        },
        threshold: 250,
        offset: {
          x: 50,
          y: 50
        },
        opacity: 0
      }
    }
  }

</script>