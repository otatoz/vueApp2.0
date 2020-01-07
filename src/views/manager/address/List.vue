<template>
    <briup-fulllayout title="常用地址">
    <van-list>
        <van-cell
            v-for="item in address"
            :key="item.id"
            :title="item.province+' '+item.city+' '+item.area+' '+item.address"
        />
    </van-list>
    <br>
    <van-button block type='info' @click="toAddressEdit">添加</van-button>

    <!-- <van-area :area-list="areaList" /> -->
    </briup-fulllayout>
</template>

<script>
import {mapState} from 'vuex'
import {get} from '../../../http/axios'
export default {
    data(){
        return {
            address:[]
        }
    },
    computed:{
        ...mapState('user',['info'])
    },
    methods:{
        loadAddress(){
            let id = this.info.id;
            get('/address/findByCustomerId?id='+id).then((res)=>{
                this.address = res.data
            })
        },
        toAddressEdit(){
            this.$router.push({
                path:'address_edit'
            })
        }
    },
    created(){
        this.loadAddress()
    }
}
</script>