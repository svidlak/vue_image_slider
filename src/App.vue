<template>
  <div id="app" v-if="ready">
    <!-- <input type="button" value="Single view" class="active" @click="slider=false"/>
    <input type="button" value="Slider view" class="" @click="slider=true"/>
    <single-view v-if="!slider":imgData="currentImg" /> -->
    <slider-view v-if="slider":imgData="imagesObj" :startingPosition="position"/>
    <div class="buttons-container">
      <ul>
        <li v-for="btn in buttonsArr" :key="btn">
            <a @click="changeImg($event, btn)" ref="btns" v-if="btn == 1" class="active">{{btn}}</a>
            <a @click="changeImg($event, btn)" ref="btns" v-else>{{btn}}</a>
        </li>
      </ul>
      <input type="button" @click="shuffle" value="shuffle" class="shuffle-btn">
    </div>
  </div>
</template>

<script>
// import SingleView from "./components/Single"
import SliderView from "./components/Slider"

export default {
  data () {
    return {
      ready: false,
      name: 'app',
      newData: null,
      numbersForIndex: [],
      imagesObj: [],
      buttonsArr: [1,2,3,4,5],
      currentImg: null,
      ///slider view///
      slider: true,
      position: 1,
    }
  },
  components:{
    // SingleView,
    SliderView
  },
  created(){
    this.numberRandomizer()
    this.$http.get('./photos.json').then((resp) => {
      this.newData = resp.body.photo
      this.dataSetup()
      this.currentImg = this.imagesObj[0]
      this.ready = true
    })
  },
  methods:{
    numberRandomizer(){
      for(let x = 0; x < 5; x++){
        this.numbersForIndex.push(Math.floor(Math.random() * 500) + 1)
      }
    },
    dataSetup(){
      this.numbersForIndex.map(ele => {
        this.imagesObj.push(this.newData[ele])
      })
    },
    shuffle(){
      this.numbersForIndex = []
      this.imagesObj = []
      this.position = 1
      this.numberRandomizer()
      this.dataSetup()
      this.resetBtns()
      this.addActive()
      this.currentImg = this.imagesObj[0]
    },
    resetBtns(){
      this.$refs.btns.forEach((ele) => {
        ele.className = ""
      })
    },
    addActive(){
      this.$refs.btns[0].className = "active"
    },
    changeImg(e, btn){
      this.position = btn
      this.resetBtns()
      e.target.classList.toggle('active')
      this.currentImg = this.imagesObj[btn-1]
    }
  },
}
</script>

<style>
html{
  height: 100%;
}

#app{
  width: 800px;
  margin: 0 auto;
}

.shuffle-btn{
    float: right;
    position: relative;
    top: -42px;
    color: #333;
    background-color: #fff;
    border-color: #ccc;
    border: 1px solid gray;
    padding: 10px;
}

ul{
  padding-left: 300px;
}
li{
  display: inline;
  list-style-type: none;
  margin-right: 5px;
}

li a{
  width: 10px;
  background: red;
  padding: 5px 10px;
  border-radius: 50%
}

.active{
  background: lightblue;
}
</style>
