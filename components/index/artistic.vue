<template>
  <section class="m-istyle">
    <dl @mouseover="over">
      <dt>有格调</dt>
      <dd :class="{active:kind==='all'}" kind="all" keyword="景点">全部</dd>
      <dd :class="{active:kind==='part'}" kind="part" keyword="美食">约会聚餐</dd>
      <dd :class="{active:kind==='spa'}" kind="spa" keyword="丽人">丽人SPA</dd>
      <dd :class="{active:kind==='movie'}" kind="movie" keyword="电影">电影演出</dd>
      <dd :class="{active:kind==='travel'}" kind="travel" keyword="旅游">品质出游</dd>
    </dl>
    <ul class="ibody">
      <li v-for="item in cur" :key="item.title">
        <el-card :body-style="{ padding: '0px' }" shadow="never">
          <img :src="item.img" class="image" />
          <ul class="cbody">
            <li class="title">{{ item.title }}</li>
            <li class="pos">
              <span>{{ item.pos }}</span>
            </li>
            <li class="price">
              ￥
              <em>{{ item.price }}</em>
              <span>/起</span>
            </li>
          </ul>
        </el-card>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  data() {
    return {
      kind: "all",
      list: {
        all: [
          // {
          //   title: "丰泽园饭店（王府井店）",
          //   img:
          //     "//p0.meituan.net/msmerchant/c08c616aa835bc7cebdc3bd17184afef312214.jpg@368w_208h_1e_1c",
          //   pos: "2人自选套餐，提供免费WiFi",
          //   price: 248
          // },
          // {
          //   title: "中央电视塔空中观景旋转餐厅",
          //   img:
          //     "//p1.meituan.net/msmerchant/7776f22c9d6fd0413b7e52441b3f74557386836.jpg@368w_208h_1e_1c",
          //   pos: "午餐+观光",
          //   price: 248
          // },
          // {
          //   title: "北京饭店诺金东33餐厅",
          //   img:
          //     "//p1.meituan.net/poi/697cf6a6e1785559a7bb31d0bf03c649110592.jpg@368w_208h_1e_1c",
          //   pos: "桌餐C，建议8-10人使用，可免费使用包间",
          //   price: 5000
          // },
          // {
          //   title: "丰泽园饭店（王府井店）",
          //   img:
          //     "//p0.meituan.net/msmerchant/c08c616aa835bc7cebdc3bd17184afef312214.jpg@368w_208h_1e_1c",
          //   pos: "2人自选套餐，提供免费WiFi",
          //   price: 248
          // },
          // {
          //   title: "中央电视塔空中观景旋转餐厅",
          //   img:
          //     "//p1.meituan.net/msmerchant/7776f22c9d6fd0413b7e52441b3f74557386836.jpg@368w_208h_1e_1c",
          //   pos: "午餐+观光",
          //   price: 248
          // },
          // {
          //   title: "北京饭店诺金东33餐厅",
          //   img:
          //     "//p1.meituan.net/poi/697cf6a6e1785559a7bb31d0bf03c649110592.jpg@368w_208h_1e_1c",
          //   pos: "桌餐C，建议8-10人使用，可免费使用包间",
          //   price: 5000
          // }
        ],
        part: [],
        spa: [],
        movie: [],
        travel: []
      }
    };
  },
  computed: {
    cur: function() {
      return this.list[this.kind];
    }
  },
  methods: {
    // 请求数据的函数，但是我们希望页面在mounted就请求数据了，所以在mounted也得写
    over: async function(e) {
      let dom = e.target;
      let tag = dom.tagName.toLowerCase();
      let self = this;
      if (tag === "dd") {
        this.kind = dom.getAttribute("kind");
        let keyword = dom.getAttribute("keyword");
        let {
          status,
          data: { count, pois }
        } = await self.$axios.get("/search/resultsByKeywords", {
          params: {
            keyword,
            city: self.$store.state.geo.position.city
          }
        });
        if (status === 200 && count > 0) {
          let r = pois
            .filter(item => item.photos.length)
            .map(item => {
              return {
                title: item.name,
                pos: item.type.split(";")[0],
                price: item.biz_ext.cost || "暂无",
                img: item.photos[0].url,
                url: "//abc.com"
              };
            });
          self.list[self.kind] = r.slice(0, 9);
        } else {
          self.list[self.kind] = [];
        }
      }
    }
  },
  async mounted(){
    let self=this;
    let {status,data:{count,pois}}=await self.$axios.get('/search/resultsByKeywords',{
      params:{
        keyword:'景点',
        city:self.$store.state.geo.position.city
      }
    })
    if(status===200&&count>0){
      let r= pois.filter(item=>item.photos.length).map(item=>{
        return {
          title:item.name,
          pos:item.type.split(';')[0],
          price:item.biz_ext.cost||'暂无',
          img:item.photos[0].url,
          url:'//abc.com'
        }
      })
      self.list[self.kind]=r.slice(0,9)
    }else{
      self.list[self.kind]=[]
    }
  }
};
</script>

<style lang="scss">
@import "@/assets/css/index/artistic.scss";
</style>
