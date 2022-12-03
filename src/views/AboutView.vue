<script lang="ts" setup>
import {useRouter} from 'vue-router'
import { ref } from 'vue'
import axios from 'axios'
const route = useRouter()
let id = route.currentRoute.value.query.id
console.log(id)

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

let lose = ref<LostObject>(new LostObject())

const load = () => {
  axios({
  url:'http://10.9.0.2:8080/object?id='+id,
  method:'get'
}).then(res => {
  lose.value = res.data
console.log(res)

})

}
load()
</script>
<template>
  <div class="about">
    {{id}}
    {{lose}}
  </div>
</template>

<style>

</style>
