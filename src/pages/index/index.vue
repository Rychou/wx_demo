<template>
<div>
  <button @click="getGrouponList">Test</button>
  <div class="weui-cells weui-cells_after-title">
    <navigator v-for="groupon in grouponList" :key="groupon.id" url="../groupons-show/main" class="weui-cell weui-cell_access" hover-class="weui-cell_active">
      <div class="weui-cell__bd">{{groupon.title}}</div>
      <div class="weui-cell__ft weui-cell__ft_in-access"></div>
    </navigator>
  </div>
  <mp-field placeholder="请输入qq" type="number" label="qq" />
  <mp-field placeholder="请输入手机号" label="手机号" type="number" vcode />
</div>
</template>

<script>
import MpField from 'mp-weui/packages/field'
export default {
  data() {
    return {
      grouponList: [{
          "id": 1,
          "title": "è‚–é‚¦",
          "pic": ""
        },
        {
          "id": 2,
          "title": "Test",
          "pic": ""
        },
        {
          "id": 3,
          "title": "Test",
          "pic": ""
        }
      ]
    }
  },
  components: {
    MpField
  },
  methods: {
    getGrouponList() {
      wx.request({
        url: "../static/api/groupons.json",
        success: function(res) {
          console.log(res.data)
          this.grouponList = res.data.grouponList
        }
      })
    }
  }
}
</script>

<style>
</style>
