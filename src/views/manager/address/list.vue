<template>
    <briup-fulllayout title="常用地址">
    <van-list>
  <van-cell
    v-for="item in addresses"
    :key="item.id"
    :title="item.province+''+item.city+' '+item.area+' '+item.address" 
  />
</van-list>
<van-button block type="default" @click="toAddressEditHandler">新增地址</van-button>
    </briup-fulllayout>
</template>
<script>
import {get} from '../../../http/axios'
import {mapState} from 'vuex'
export default {
    data(){
        return{
            addresses:[]
        }
    },
    computed:{
...mapState("user",["info"])
    },
    created(){
        this.loadAddress();
    },
    methods:{
        loadAddress(){
            let id=this.info.id;
            let url="/address/findByCustomerId?id="+id;
            get(url).then((response)=>{
                this.addresses=response.data;
            })
        },   
        toAddressEditHandler(){
            this.$router.push("/manager/address_edit");
        }
    }
    }
</script>
<style scoped>
</style>