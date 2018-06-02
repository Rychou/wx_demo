<template>
    <div>
        <button @click="getGrouponList">Test</button>
        <div class="weui-cells weui-cells_after-title">
            <navigator v-for="groupon in grouponList" :key="groupon.id" url="../groupons-show/main" class="weui-cell weui-cell_access" hover-class="weui-cell_active">
            <div class="weui-cell__bd">{{groupon.title}}</div>
            <div class="weui-cell__ft weui-cell__ft_in-access"></div>
            </navigator>
        </div>
    </div>
</template>

<script>
// import card from '@/components/card'
/*eslint-disable*/
export default {
    data(){
        return {
            grouponList:[
                {
                    "id":1,
                    "title":"肖邦",
                    "pic":""    
                },
                {
                    "id":2,
                    "title":"Test",
                    "pic":""    
                },
                {
                    "id":3,
                    "title":"Test",
                    "pic":""    
                }
    ]}
    },
    methods:{
        getGrouponList(){
            wx.request({
                url:"../static/api/groupons.json",
                success:function(res){
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
