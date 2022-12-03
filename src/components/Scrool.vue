<template>
  <ul v-infinite-scroll="load" class="infinite-list" style="overflow: auto">
    <li v-for="i in lose" :key="i.id" class="infinite-list-item">
      <el-card :body-style="{ padding: '0px' }">
        <img
          src="https://shadow.elemecdn.com/app/element/hamburger.9cf7b091-55e9-11e9-a976-7f4d0b07eef6.png"
          class="image"
        />
        <div style="padding: 40px">
          <span>{{i.title}}</span>
          <div class="bottom">
            <time class="time">{{ i.finddate.getFullYear()+'-'+i.finddate.getMonth()+'-'+i.finddate.getDate()}}</time>
            <el-button @click="topage(i.id)" text class="button" type="success" plain>详情</el-button>
          </div>
        </div>
      </el-card>
    </li>
  </ul>
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import axios from 'axios'
import { useRouter } from 'vue-router'
const router = useRouter()

interface ILostObject{
  id : number,
  title : string,
  picurl : string,
  finddate : Date,
  location : string,
  remarkable : string,
  finish : boolean
}
class LostObject implements ILostObject{
  id !: number;
  title !: string;
  picurl !: string;
  finddate !: Date;
  location !: string;
  remarkable !: string;
  finish !: boolean;
}
class LostObjects {
  records !: LostObject[];
  total !: number;
  current !: number;
  orders !: [];
  optimizeCountSql !: boolean;
  hitCount !: boolean;
  countId !: string;
  maxLimit !: string;
  searchCount !: boolean;
  pages !: number;
}
let obj = ref(new LostObjects())
let lose = ref<LostObject[]>([])
const count = ref(0)

const load = () => {
  count.value += 2
  axios({
  url:'http://10.9.0.2:8080/objects?current='+count.value/2+'&size=2',
  method:'get'
}).then(res => {
  obj.value = res.data
  obj.value.records[0].finddate = new Date(obj.value.records[0].finddate)
  obj.value.records[1].finddate = new Date(obj.value.records[1].finddate)

  lose.value.push(obj.value.records[0])
  lose.value.push(obj.value.records[1])
  
})

}



function topage(i:number) {
  router.push("/about?id="+i)

}
</script>

<style>
.infinite-list {
  height: 800px;
  padding: 0;
  margin: 0;
  list-style: none;
}
.infinite-list .infinite-list-item {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 450px;
  
  margin: 0px;
  color: var(--el-color-primary);
}
.infinite-list .infinite-list-item + .list-item {
  margin-top: 10px;
}
.bottom {
  margin-top: 13px;
  line-height: 12px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

</style>
