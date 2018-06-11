<template>
<div>
  <button @click="getGrouponList">Test</button>
  <div class="weui-cells weui-cells_after-title">
    <!-- 这是微信原生组件，但是在mpvue中使用方式有所不同 具体可见https://blog.csdn.net/weixin_36934930/article/details/80173023 -->
    <scroll-view :scroll-y="true" :style="{'height': '400px'}" @scrolltolower="loadMore">
      <navigator v-for="groupon in grouponList" :key="groupon.id" url="../groupons-show/main" class="weui-cell weui-cell_access" hover-class="weui-cell_active">
        <div class="weui-cell__bd">{{groupon.title}}</div>
        <div class="weui-cell__ft weui-cell__ft_in-access"></div>
      </navigator>
      <!-- 在MP-WeUI的组件里使用微信原生的hidden属性会有问题，这里在外面套一层div使用hidden -->
      <div :hidden="!showLoadMore">
        <mp-loadmore type="loading" />
      </div>
    </scroll-view>
    
  </div>
</div>
</template>

<script>
import MpLoadmore from 'mp-weui/packages/loadmore'

export default {
  data() {
    return {
      grouponList:[],
      showLoadMore:false
    }
  },
  components: {
    MpLoadmore
  },
  mounted:function(){
    wx.request({
            url: 'https://easy-mock.com/mock/5b19e8a6966c7b5e64d9cb0a/api/grouponList', //开发者服务器接口地址",
            method: 'GET',
            dataType: 'json', //如果设为json，会尝试对返回的数据做一次 JSON.parse
            success: res => {
              console.log(res.data.grouponList)
              this.grouponList=res.data.grouponList
              console.log(this.grouponList)
            },
          });

  },
  methods:{
    loadMore(){
      this.showLoadMore=true
      wx.request({
            url: 'https://easy-mock.com/mock/5b19e8a6966c7b5e64d9cb0a/api/grouponList', //开发者服务器接口地址",
            method: 'GET',
            dataType: 'json', //如果设为json，会尝试对返回的数据做一次 JSON.parse
            success: res => {
              setTimeout(()=>{
                this.grouponList=[...this.grouponList,...res.data.grouponList]
                this.showLoadMore=false
              },2000)
              
            },
          });
    }
  }
}
</script>

<style>
</style>
