<template>
<div>
    <!-- Slider -->
  <div v-for="(value, key) in imagesObj" :key="key">
      <img :src="value.img" style="display:none;">
      <div v-if="key == startingPosition-1">
        <div class="main-wrapper" v-bind:style="{background: 'url('+value.img+') center center', backgroundSize: 'cover'}" ref="cover">
            <h3>{{value.title}}</h3>
            <p v-if="value.description">{{value.description}}</p>
          </div>
        </div>
  </div>    
</div>
</template>

<script>
export default {
    props: ["imgData","startingPosition"],
    data(){
        return{
            imagesObj: null,
            position: null,
        }
    },
    created(){
        this.imagesObj = this.$props.imgData
        this.position = this.$props.startingPosition
        
    },
    updated(){
        this.imagesObj = this.$props.imgData
    }
}
</script>

<style>
.main-wrapper{
    margin: 0 auto;
    width: 100%;
    height: 400px;
    position: relative;
}

.main-wrapper h3{
    background: rgba(0,0,0,0.5);
    padding: 10px;
    color: white;
}

.main-wrapper p{
    position: absolute;
    bottom: 0;
    background: rgba(0,0,0,0.5);
    margin: 0;
    padding: 10px;
    color: white;
    font-size: 20px;
    width: 780px;
}
</style>
