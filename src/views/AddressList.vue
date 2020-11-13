<template>
    <div>
        <van-address-list
                v-model="chosenAddressId"
                :list="list"
                default-tag-text="默认"
                @add="onAdd"
                @edit="onEdit"
                @select="onselect"
        />
    </div>
</template>

<script>
    import { Toast } from 'vant';
    export default {
        data() {
            return {
                chosenAddressId: 0,
                list: [
                    {
                        areaCode:'440303',
                        id:21,
                        name:'陈一渐',
                        tel:'15123336960',
                        address: '重庆市九龙坡区'
                    },
                    {
                        areaCode:'330104',
                        id:24,
                        name:'张三',
                        tel:'15112341234',
                        address: '重庆市沙坪坝区'
                    }
                ]
            }
        },
        created(){
            // const _this = this
            // axios.get('http://localhost:8181/address/list').then(function (resp) {
            //     _this.list = resp.data.data
            // })
        },
        methods: {
            onAdd() {
                this.$router.push('/addressNew')
            },
            onEdit(item) {
                let data = JSON.stringify(item)
                this.$router.push({path:'/addressEdit',query:{item:data}})
            },
            onselect(item){
                // let orderForm = {
                //     name: item.name,
                //     tel: item.tel,
                //     address: item.address,
                //     specsId: this.$store.state.specsId,
                //     quantity: this.$store.state.quantity
                // }
                // const _this = this
                // axios.post('http://localhost:8181/order/create',orderForm).then(function (resp) {
                //     if(resp.data.code == 0){
                        let instance = Toast('下单成功');
                        setTimeout(() => {
                            instance.close();
                            this.$router.push('/detail')
                            // _this.$router.push('/detail?orderId='+resp.data.data.orderId)
                        }, 1000)
                //     }
                // })
            }
        }
    }
</script>