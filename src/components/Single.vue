<template>
  <div>
      Single
        <div class="main-wrapper" v-bind:style="{background: 'url('+imgData.img+') center center', backgroundSize: 'cover'}" ref="cover">
          <h3>{{imgData.title}}</h3>
          <p v-if="imgData.description">{{imgData.description}}</p>
        </div>
  </div>
</template>

<script>
export default {
    props: ["imgData"],
    updated(){
        //Some bug with Vue.js not applying specificly backgroundSize:cover, so thats my workaround
        this.$refs.cover.style.backgroundSize = 'cover'
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
