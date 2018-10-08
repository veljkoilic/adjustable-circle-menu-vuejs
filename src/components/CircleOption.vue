<template>
    <transition name="explode">
        <div class="circleOption" :class="position">
              <div :class="[selected ?  'selected': '' , 'circle']" :style="{backgroundColor: color}" @click="$parent.$emit('selected', {id, color, icon, iconColor, selected})" >
                  <i class="fas" :class=" 'fa-' + icon" :style="{color: iconColor}"></i>
              </div>
          </div>
    </transition>
</template>

<script>
export default {
  name: 'CircleOption',
    props:{
      id: String,
      position: String,
      color: String,
      icon: String,
      iconColor: String,
      selected: Boolean
    }
}
</script>

<style scoped lang="scss">
    .circleOption {
        display: flex;


        &:hover{
            cursor: pointer;
            transform: scale(1.1);
            transition: 1s;
        }
        .circle {
            width: 50%;
            height: 50%;
            border-radius: 200px;
            display: flex;
            justify-content: center;
            align-items: center;
            i{
                font-size: 3em;
                backface-visibility: hidden;
            }
        }
        .selected{
            padding: 20px;
        }
    }
    .centered{
        justify-content: center;
        align-items: center;
    }
    .a1{
        justify-content: flex-end;
        align-items: flex-end;
    }
    .a3{
        align-items: flex-end;
    }
    .c1{
        justify-content: flex-end;
        align-items: flex-start;
    }
    .c3{
        align-items: flex-start;
    }
</style>
