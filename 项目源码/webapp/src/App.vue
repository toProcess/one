<template>
  <div>
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <a v-link="{path:'/goods'}">商品</a>
      </div>
      <div class="tab-item">
        <a v-link="{path:'/ratings'}">评论</a>
      </div>
      <div class="tab-item">
        <a v-link="{path:'/seller'}">商家</a>
      </div>
    </div>
    <router-view :seller="seller" keep-alive></router-view>
  </div>
</template>

<script type="text/ecmascript-6">
  import {urlParse} from 'common/js/util';
  import header from 'components/header/header.vue';

  // 项目打包后mock无法请求数据，静态数据
  import { data } from 'common/js/data.js';

//  const ERR_OK = 0;

  export default {
    data() {
      return {
        seller: {
          id: (() => {
            let queryParam = urlParse();
            return queryParam.id;
          })()
        }
      };
    },
    created() {
//   获取seller数据
//      this.$http.get('/api/seller?id=' + this.seller.id).then((response) => {
//        response = response.body;
//        if (response.errno === ERR_OK) {
//          this.seller = Object.assign({}, this.seller, response.data);
//        }
//      });
      const seller = data.seller;
      this.seller = Object.assign({}, this.seller, seller);
    },
    components: {
      'v-header': header
    }
  };

</script>

<style lang="stylus" rel="stylesheet/stylus">

  .tab
   display: flex
   width: 100%
   height: 40px
   line-height: 40px
   .tab-item
    flex: 1
    text-align: center
    & > a
      display: block
      color: rgb(77, 85, 93)
      &.active
       color: rgb(240, 20, 20)
</style>
