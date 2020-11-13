<template>
  <div>
    <van-tabs @click="onClick" sticky line-width="25%" title-active-color="#e32dab" color="e32dab" >
      <!--循环遍历标题栏-->
      <van-tab v-for="index in categories.length"  :title="categories[index-1].name" ></van-tab>

    </van-tabs>
    <van-card v-for="(item,index) in phones"
            :price="item.price"
            :desc="item.desc"
            :title="item.title"
            :thumb="item.thumb"
    >
      <template #tags>
        <van-tag v-for="tag in item.tag"color="#f2826a" style="margin-left: 5px;">{{tag.name}}</van-tag>
      </template>
      <template #footer>
        <van-button round type="info" size="mini" @click="buy">购买</van-button>
      </template>
    </van-card>
    <van-sku
            v-model="show"
            :sku="sku"
            :goods="goods"
            :hide-stock="sku.hide_stock"
            @buy-clicked="onBuyClicked"
            :show-add-cart-btn="false"
    />

<!--    <van-row>-->
<!--      <van-col span="24">-->
<!--        <van-tabs @click="onClick" sticky title-active-color="#E32DAB" color="#E32DAB" :line-width="100" :line-height="2">-->

<!--&lt;!&ndash;          <van-tab v-for="index in categories.length" :title="categories[index-1].name" class="tab">&ndash;&gt;-->

<!--&lt;!&ndash;            <van-card v-for="(item,index) in phones"&ndash;&gt;-->
<!--&lt;!&ndash;                      :price="item.price"&ndash;&gt;-->
<!--&lt;!&ndash;                      :desc="item.desc"&ndash;&gt;-->
<!--&lt;!&ndash;                      :title="item.title"&ndash;&gt;-->
<!--&lt;!&ndash;                      :thumb="item.thumb"&ndash;&gt;-->
<!--&lt;!&ndash;            >&ndash;&gt;-->
<!--&lt;!&ndash;              <template #tags>&ndash;&gt;-->
<!--&lt;!&ndash;                <van-tag v-for="tag in item.tag" color="#f2826a" style="margin-left: 5px;">{{tag.name}}</van-tag>&ndash;&gt;-->
<!--&lt;!&ndash;              </template>&ndash;&gt;-->
<!--&lt;!&ndash;              <template #footer>&ndash;&gt;-->
<!--&lt;!&ndash;                <van-button round type="info" size="mini" @click="buy(index)">购买</van-button>&ndash;&gt;-->
<!--&lt;!&ndash;              </template>&ndash;&gt;-->
<!--&lt;!&ndash;            </van-card>&ndash;&gt;-->


<!--&lt;!&ndash;          </van-tab>&ndash;&gt;-->
<!--        </van-tabs>-->
<!--      </van-col>-->
<!--    </van-row>-->

<!--    <van-sku-->
<!--            v-model="show"-->
<!--            :sku="sku"-->
<!--            :goods="goods"-->
<!--            :hide-stock="sku.hide_stock"-->
<!--            @buy-clicked="onBuyClicked"-->
<!--    >-->
<!--      <template #sku-actions="props">-->
<!--        <div class="van-sku-actions">-->

<!--          &lt;!&ndash; 直接触发 sku 内部事件，通过内部事件执行 onBuyClicked 回调 &ndash;&gt;-->
<!--          <van-button-->
<!--                  square-->
<!--                  size="large"-->
<!--                  type="danger"-->
<!--                  @click="props.skuEventBus.$emit('sku:buy')"-->
<!--          >-->
<!--            买买买-->
<!--          </van-button>-->
<!--        </div>-->
<!--      </template>-->
<!--    </van-sku>-->

  </div>


</template>

<script>
  import {
    Toast,
    PullRefresh,
    Swipe,
    SwipeItem
  } from 'vant';
  export default {
    data(){
      return{
        categories:[
          {
            name:'魅焰红',
            type:1
          },
          {
            name:'极光蓝',
            type:2
          },
          {
            name:'铂光金',
            type:3
          },
          {
            name:'幻夜黑',
            type:4
          }
        ],
        active: 0,
        phones:[
          {
            id:1,
            title:'Honor 8A',
            price:'2800.00',
            desc:'魅焰红',
            tag:[
              {
                name:'720P珍珠屏'
              },
              {
                name:'Micro USB接口'
              }
            ],
            thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
          },
          {
            id:5,
            title:'HUAWEI nova 5 Pro',
            price:'5450.00',
            desc:'魅焰红',
            tag:[
              {
                name:'内存3GB'
              },
              {
                name:'EMUI9 Lite'
              }
            ],
            thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
          },
          {
            id:9,
            title:'SAMSUNG G S10',
            price:'7254.00',
            desc:'魅焰红',
            tag:[
              {
                name:'720P珍珠屏'
              },
              {
                name:'存储32GB'
              }
            ],
            thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
          },
          {
            id:13,
            title:'VIVO X27',
            price:'2888.00',
            desc:'魅焰红',
            tag:[
              {
                name:'F/1.8光圈'
              },
              {
                name:'Micro USB接口'
              }
            ],
            thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
          },
          {
            id:17,
            title:'Meizu 16s',
            price:'1220.00',
            desc:'魅焰红',
            tag:[
              {
                name:'720P珍珠屏'
              },
              {
                name:'Micro USB接口'
              }
            ],
            thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
          }
        ],
        show: true,
        sku:{
          tree:[
            {
              k: '规格',
              v:[
                {
                  id:1,
                  name:'32GB',
                  imgUrl:'https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png',
                  previewImgUrl:'https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png'
                },
                {
                  id:2,
                  name:'64GB',
                  imgUrl:'https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png',
                  previewImgUrl:'https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png'
                }
              ],
              k_s:'s1',
              largeImageMode: true,
            }
          ],
          list: [
            {
              s1: 1,
              price:280000,
              stock_num:5
            },
            {
              s1: 2,
              price:320000,
              stock_num:5
            },
          ],
          price:'2800.00',
          stock_num:10,
          none_sku:false,
          hide_stock:false
        },
        goods:{
          picture:'https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png'
        }
      }
    },
    created(){

    },
    methods:{
      buy(index){
        this.show=true
      },
      onBuyClicked(item){
        console.log(item)
        this.$store.state.specsId=item.selectedSkuComb.s1
        this.$store.state.quantity=item.selectedNum
        this.$router.push('/addressList')
      },
      onClick(index){
        switch (index) {
          case 0:
            this.phones=[
              {
                id:1,
                title:'Honor 8A',
                price:'2800.00',
                desc:'魅焰红',
                tag:[
                  {
                    name:'720P珍珠屏'
                  },
                  {
                    name:'Micro USB接口'
                  }
                ],
                thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
              },
              {
                id:5,
                title:'HUAWEI nova 5 Pro',
                price:'5450.00',
                desc:'魅焰红',
                tag:[
                  {
                    name:'内存3GB'
                  },
                  {
                    name:'EMUI9 Lite'
                  }
                ],
                thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
              },
              {
                id:9,
                title:'SAMSUNG G S10',
                price:'7254.00',
                desc:'魅焰红',
                tag:[
                  {
                    name:'720P珍珠屏'
                  },
                  {
                    name:'存储32GB'
                  }
                ],
                thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
              },
              {
                id:13,
                title:'VIVO X27',
                price:'2888.00',
                desc:'魅焰红',
                tag:[
                  {
                    name:'F/1.8光圈'
                  },
                  {
                    name:'Micro USB接口'
                  }
                ],
                thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
              },
              {
                id:17,
                title:'Meizu 16s',
                price:'1220.00',
                desc:'魅焰红',
                tag:[
                  {
                    name:'720P珍珠屏'
                  },
                  {
                    name:'Micro USB接口'
                  }
                ],
                thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
              }
            ]
            break;
          case 1:
            this.phones=[
              {
                id:2,
                title:'Honor 10 青春版',
                price:'2800.00',
                desc:'极光蓝',
                tag:[
                  {
                    name:'720P珍珠屏'
                  },
                  {
                    name:'EMUI9 Lite'
                  }
                ],
                thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
              },
              {
                id:6,
                title:'HUAWEI P30',
                price:'8700.00',
                desc:'极光蓝',
                tag:[
                  {
                    name:'720P珍珠屏'
                  },
                  {
                    name:'内存3GB'
                  }
                ],
                thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
              },
              {
                id:10,
                title:'OPPO K3',
                price:'2889.00',
                desc:'极光蓝',
                tag:[
                  {
                    name:'存储32GB'
                  },
                  {
                    name:'Micro USB接口'
                  }
                ],
                thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
              },
              {
                id:14,
                title:'Iphone 6',
                price:'5678.00',
                desc:'极光蓝',
                tag:[
                  {
                    name:'720P珍珠屏'
                  },
                  {
                    name:'F/1.8光圈'
                  }
                ],
                thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
              },
              {
                id:18,
                title:'Iphone X',
                price:'6770.00',
                desc:'极光蓝',
                tag:[
                  {
                    name:'F/1.8光圈'
                  },
                  {
                    name:'Micro USB接口'
                  }
                ],
                thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
              }
            ]
            break;
          case 2:
            this.phones=[
              {
                id:3,
                title:'Honor V20',
                price:'3450.00',
                desc:'铂光金',
                tag:[
                  {
                    name:'2+1独立三卡槽'
                  }
                ],
                thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
              },
              {
                id:7,
                title:'HUAWEI P30 Pro',
                price:'8988.00',
                desc:'铂光金',
                tag:[
                  {
                    name:'720P珍珠屏'
                  },
                  {
                    name:'Micro USB接口'
                  }
                ],
                thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
              },
              {
                id:11,
                title:'Iphone XR',
                price:'9888.00',
                desc:'铂光金',
                tag:[
                  {
                    name:'1300万像素'
                  },
                  {
                    name:'Micro USB接口'
                  }
                ],
                thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
              },
              {
                id:15,
                title:'Iphone 7',
                price:'5576.00',
                desc:'铂光金',
                tag:[
                  {
                    name:'720P珍珠屏'
                  },
                  {
                    name:'1300万像素'
                  }
                ],
                thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
              },
              {
                id:19,
                title:'HUAWEI P20',
                price:'5580.00',
                desc:'铂光金',
                tag:[
                  {
                    name:'1300万像素'
                  },
                  {
                    name:'Micro USB接口'
                  }
                ],
                thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
              }
            ]
            break;
          case 3:
            this.phones=[
              {
                id:4,
                title:'HUAWEI Mate 20 Pro',
                price:'4550.00',
                desc:'幻夜黑',
                tag:[
                  {
                    name:'内存3GB'
                  },
                  {
                    name:'EMUI9 Lite'
                  }
                ],
                thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
              },
              {
                id:8,
                title:'HUAWEI 畅想9 Plus',
                price:'2760.00',
                desc:'幻夜黑',
                tag:[
                  {
                    name:'内存3GB'
                  },
                  {
                    name:'存储32GB'
                  }
                ],
                thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
              },
              {
                id:12,
                title:'MI 8',
                price:'5888.00',
                desc:'幻夜黑',
                tag:[
                  {
                    name:'F/1.8光圈'
                  },
                  {
                    name:'Micro USB接口'
                  }
                ],
                thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
              },
              {
                id:16,
                title:'Iphone 8',
                price:'6212.00',
                desc:'幻夜黑',
                tag:[
                  {
                    name:'内存3GB'
                  },
                  {
                    name:'F/1.8光圈'
                  }
                ],
                thumb:"https://shopstatic.vivo.com.cn/vivoshop/commodity/31/10005931_1603089876415_750x750.png"
              }
            ]
            break;
        }
      }
    }
    // comments:{
    //   [PullRefresh.name]: PullRefresh,
    //   [Swipe.name]: Swipe,
    //   [SwipeItem.name]: SwipeItem
    // },
    // data() {
    //   // return {
    //   //   categories: '',
    //   //   phones: '',
    //   //   show: true,
    //   //   sku: '',
    //   //   goods: ''
    //   // }
    // },
    // created(){
    //   const _this = this
    //   axios.get('http://localhost:8181/phone/index').then(function (resp) {
    //     _this.phones = resp.data.data.phones
    //     _this.categories = resp.data.data.categories
    //   })
    // },
    // methods: {
    //   onClick(index) {
    //     const _this = this
    //     axios.get('http://localhost:8181/phone/findByCategoryType/'+this.categories[index].type).then(function (resp) {
    //       _this.phones = resp.data.data
    //     })
    //   },
    //   buy(index){
    //     this.show = true
    //     const _this = this
    //     axios.get('http://localhost:8181/phone/findSpecsByPhoneId/'+this.phones[index].id).then(function (resp) {
    //       _this.goods = resp.data.data.goods
    //       _this.sku = resp.data.data.sku
    //     })
    //   },
    //   onBuyClicked(item){
    //     this.$store.state.specsId = item.selectedSkuComb.s1
    //     this.$store.state.quantity = item.selectedNum
    //     this.$router.push('/addressList')
    //   }
    // }
  }
</script>