<template>
  <div>
    <div class="title">国外疫情地图</div>
    <!-- 地图容器 -->
    <div id="main" style="width: 7.5rem; height: 7rem"></div>
  </div>
</template>

<script>
import api from "../api/index";
export default {
  name: "WorldMap",
  mounted() {
    //-------------------------
    api.getWorldData().then((res) => {
      let world = res.data.retdata;
      let arr = []; //累计
      for (let i = 0; i < world.length; i++) {
        let obj = {};
        obj.name = world[i].xArea;
        obj.value = world[i].confirm; //累计确诊人数   curConfirm现在确诊人数
        arr.push(obj);
      }
      this.$myChart.worldMap("main", arr);
    });
  },
};
</script>

<style lang='less' scoped>
.title {
  margin: 0.2rem;
  padding-top: 0.2rem;
  border-top: 1px solid #eee;
}
.title::before {
  content: "";
  border-left: 0.1rem solid rgb(9, 60, 202);
  font-size: 0.26rem;
  margin-right: 0.1rem;
}
#main {
  background: #f5f5f5;
}
</style>