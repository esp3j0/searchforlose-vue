<script lang="ts">
interface ILostObject{
  id : number,
  title : string,
  picurl : string,
  finddate : string,
  location : string,
  type : string,
  remarktable : string,
  finish : boolean
}
class LostObject implements ILostObject{
  id !: number;
  title !: string;
  picurl !: string;
  finddate !: string;
  location !: string;
  type !: string;
  remarktable !: string;
  finish !: boolean;
}
export default {
    props: {
        alose : LostObject,
    }
  }
</script>
<script lang="ts" setup>
import {useRouter} from 'vue-router'
let route = useRouter()
function ret(){
    route.back()
}
</script>
<template>
    <div>
        <el-image src="https://creepey-1306653668.cos.ap-shanghai.myqcloud.com/note/image-20221203095511763.png"></el-image>
    </div>
    <br>
    <div>
        <el-card class="box-card">
            <template #header>
              <div class="card-header">
                <span>{{alose?.title}}</span>
                <el-button class="button" text type="success">认领</el-button>
              </div>
            </template>
            <div :key="alose?.id" class="text item">{{ '位置: ' + alose?.location }}</div>
            
            <div :key="alose?.id" class="text item">{{ '备注: ' + alose?.remarktable }}</div>
            
            <div :key="alose?.id" class="text item">{{ '发现时间: ' + alose?.finddate.split("T",1)[0] }}</div>
          </el-card>
    </div>
    <br>
    <div>
        <el-button @click="ret()" class="butt" type="primary" plain>返回</el-button>
    </div>

</template>
  
  <style>
  .card-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  .text {
    font-size: 14px;
  }
  
  .item {
    margin-bottom: 18px;
  }
  
  .box-card {
    width: 300px;
  }
  .butt {
    width: 300px;
    height: 45px;
  }
  </style>
  