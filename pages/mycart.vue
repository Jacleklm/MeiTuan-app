<template>
  <div class="page-cart">
    <div class="mycar">
      不用Element UI，纯手写的购物车 ：
      <div class="wrapper" v-for="item in goods" :key="item.title">
        <!-- 第一个注意点，把checkbox的状态v-model到item的属性 -->
        <input type="checkbox" v-model="item.choose"/>
        <img :src="item.img" />
        <sapn class="price">单价：{{ item.price }}</sapn>
        <sapn class="count">数量：
          <!-- 第二个注意点，这里可以把@click直接写在这里，而不是methods中，这样能拿到item -->
          <button @click="item.count--">-</button> {{ item.count }} <button @click="item.count++">+</button>
        </sapn>
        <sapn class="Allprice">总价：{{ item.price *  item.count}}</sapn>
      </div>
      <strong>应付金额：￥ {{mytotal }}</strong>
      <p></p>
      <button @click="test">提交</button>
    </div>
  </div>
</template>

<script>
import counter from "@/components/mycart/counter.vue";
export default {
  components: {
    counter
  },
  data() {
    return {
      goods: [
        {
          title: "ikbc机械键盘",
          price: 419,
          count: 1,
          img:
            "https://img.alicdn.com/bao/uploaded/i3/3446533752/O1CN01cEDlFs1daSZuP7Fzo_!!3446533752.jpg_80x80.jpg",
        },
        {
          title: "羽绒服",
          price: 529,
          count: 1,
          img:
            "https://img.alicdn.com/bao/uploaded/i1/188124207/O1CN01JUv0HN1gwqoa36Lu1_!!188124207.jpg_80x80.jpg",
        },
        {
          title: "华为 nova 5",
          price: 1999,
          count: 1,
          img:
            "https://img.alicdn.com/bao/uploaded/i4/2838892713/O1CN01iv6azS1Vub3xziReN_!!2838892713.jpg_80x80.jpg",
        }
      ]
    };
  },
  methods: {
    test: () => {
      
    }
  },
  computed: {
    mytotal() {
      let total = 0;
      this.goods.forEach(item => {
        if (item.choose) {
          total += item.price * item.count;
        }
      });
      return total;
    }
  }
};
</script>

<style lang="scss">
.mycar {
  padding-left: 20px;
  .wrapper {
    height: 100px;
    line-height: 100px;
    border: solid 1px black;
    margin-top: 10px;

    img {
      vertical-align: middle;
      margin: 0 20px;
    }
    sapn {
      vertical-align: middle;
    }
    .count {
      margin-left: 200px;
    }
    .Allprice {
      margin-left: 300px;
    }
  }
}
</style>
