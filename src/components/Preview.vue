<template>
  <div id="wrapper">
  <banner :listImgC="result" id="banner"></banner>
  <pagination :names="tags" :indexC="currentIndex"  @indexUpdate="updateIndex"></pagination>
  <detail :detailC="detail"></detail>  
  </div>
</template>

<script>
import Banner from "./Banner.vue";
import Pagination from "./Pagination.vue";
import Detail from './Detail.vue'
export default {
  name: "Preview",
  components: { Pagination,Banner,Detail },
  data:function(){
      return {
          tags:[],
          listImg:[],
          currentIndex:0,
          detail:{}
      }
  },
  computed:{
     result:function() {
         return this.listImg[this.currentIndex]
     }
  },
  methods:{
      updateIndex:function(index){
          this.currentIndex = index
      }
  },
  created() {
    var self = this;
    this.$http.get("api/user/houseType/detail?id=1").then(function(response) {
      // console.log(response.data.data.baseInfo)
      self.detail = response.data.data.baseInfo
      response.data.data.imgInfo.forEach(element => {
        self.tags.push(element.type_name)
        self.listImg.push(element.data)
      });
    });
  },

};
</script>
<style scoped>
#banner{
    width: 6.79rem;
    height:4.96rem;
}
</style>
