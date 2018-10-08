<template>
    <div>
        <div class="settings">
            <div>
                <h3>Backgroud color</h3>
                <input @blur="searchAndChange(selectionId, circles)" v-model="newColor" type="text">
            </div>
            <div>
                <h3>Icon</h3>
                <input @blur="searchAndChange(selectionId, circles)" v-model="newIcon" type="text">
            </div>
            <div>
                <h3>Color of icons</h3>
                <input @blur="searchAndChange(selectionId, circles)" v-model="newIconColor" type="text">
            </div>
        </div>
        <p>Click on bubbles to change them</p>
        <p>RGB, hex and words supported for colors</p>
        <p>Icons from font-awesome</p>
            <div class="circleMenu">
          <div class="mainWrap">
                <div @click="show = !show" class="mainCircle"><i class="fas fa-asterisk" :style="{color: iconColor}" :class="[show ? 'rotate' : 'rotate2']"></i></div>
          </div>
          <CircleOption
          v-if="show"
          :key="circle.color"
          v-for="circle in circles"
          :id="circle.id"
          :position="circle.position"
          :color="circle.color"
          :icon="circle.icon"
          :selected="circle.selected"
          :iconColor="iconColor"/>
      </div>
    </div>
</template>

<script>
import CircleOption from './CircleOption'
export default {
  name: 'CircleMenu',
    components:{
      CircleOption
    },
    methods:{
        searchAndChange(myId, myArray){
            for (let i=0; i < myArray.length; i++) {
                myArray[i].selected = false
                if (myArray[i].id === myId) {
                    myArray[i].color = this.newColor
                    myArray[i].icon = this.newIcon
                    myArray[i].selected = true
                    this.iconColor = this.newIconColor

                }
            }
        },
        selectOne(myId, myArray){
            for (let i=0; i < myArray.length; i++) {
                if (myArray[i].id === myId) {
                    myArray[i].selected = true

                }
            }
        }

    },
    mounted(){
      this.$on('selected', (data)=>{
          this.selectionId = data.id
          this.newColor = data.color
          this.newIcon = data.icon
          this.newIconColor = data.iconColor
          this.circles.forEach(function (circle){
              circle.selected = false
          })
          this.selectOne(this.selectionId, this.circles)
          this.searchAndChange(this.selectionId, this.circles)
      })
    },
    data(){
      return{
          show: false,
          iconColor: "white",
          selectionId:'a1',
          newColor: 'New Color',
          newIcon: 'New Icon',
          newIconColor: 'New icon color',
          circles:[
              {
                  id: 'Which',
                  position: "a1",
                  color: "#33658A",
                  icon: "angry",
                  selected: false
              },
              {
                  id: 'a2',
                  position:"centered",
                  color: "#F6AE2D",
                  icon:"at",
                  selected: false
              },
              {
                  id: 'a3',
                  position:"a3",
                  color: "#758E4F",
                  icon:"bell",
                  selected: false
              },
              {
                  id: 'b1',
                  position:"centered",
                  color: "#F26419",
                  icon:"box-open",
                  selected: false
              },
              {
                  id: 'b3',
                  position:"centered",
                  color: "#392F5A",
                  icon:"calendar",
                  selected: false
              },
              {
                  id: 'c1',
                  position:"c1",
                  color: "#285943   ",
                  icon:"camera-retro",
                  selected: false
              },
              {
                  id: 'c2',
                  position:"centered",
                  color: "#A93F55",
                  icon:"check",
                  selected: false
              },
              {
                  id: 'c3',
                  position:"c3",
                  color: "#19323C",
                  icon:"clock",
                  selected: false
              }
          ]
      }
    }
}
</script>

<style scoped lang="scss">
    @media only screen and (max-width: 900px) {
        .settings{
            grid-template-columns: 1fr !important;
            margin-bottom: 20px;
        }
        .circleMenu{
            top: 80%;
        }

    }
.settings{
    margin: 30px 30px;
    padding: 0 20px;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    div{
        text-align: justify;
        margin: 0 auto;
    }
    input{
        width: 200px;
        padding: 20px 20px 20px 20px;
        font-size: 18px;
        border: none;
        border-bottom: 1px solid white;
        font-family: 'Work Sans', sans-serif;
        font-weight: 900;
        color: #fff;
        background: lighten(#3A393F, 10);
        border-radius: 50px;
        text-transform: uppercase;
        &:focus{
            outline: none;
            border-bottom: 1px solid black;
        }
    }
}
p{
     font-size: 20px;
     color: #fff;
     text-align: center;
     font-weight: bold;
 }
.circleMenu{
    width: 500px;
    height: 500px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr 1fr;
    .mainWrap {
        grid-column-start: 2;
        grid-row-start: 2;
        display: flex;
        justify-content: center;
        align-items: center;
        .mainCircle {
            width: 100px;
            height: 100px;
            background: red;
            border-radius: 200px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 40px;
            transform: rotate(-360deg);
            transition: 2s all;
            cursor: pointer;
        }
    }
}
.explode-enter-active, .explode-leave-active{
 transition: all 0.7s ease;
}
.explode-enter, .explode-leave-to{
 transform: scale(30);
    }
.explode-leave-to{
    opacity: 0;
}
.rotate{
    transform: rotate(360deg);
    transition: 2s all;
}
.rotate2{
    transform: rotate(-360deg);
    transition: 2s all;
}
</style>
