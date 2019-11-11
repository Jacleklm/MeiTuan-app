<template>
  <div class="search-panel">
    <el-row class="m-header-searchbar">
      <el-col
        :span="3"
        class="left"
      >
       <img
        src="//s0.meituan.net/bs/fe-web-meituan/fa5f0f0/img/logo.png"
        alt="美团"
        >
      </el-col>
      <el-col
        :span="15"
        class="center">
        <div class="wrapper">
          <el-input
            placeholder="搜索商家或地点"
          >
            1
          </el-input>
          <button class="el-button el-button--primary"><i class="el-icon-search"/></button>
          <!-- 这里是focus后搜索框出现的部分和输入后出现的推荐部分 -->
          <dl
            style="display:none"
            class="hotPlace">
            <dt>热门搜索</dt>
            <dd>火锅</dd>
            <dd>火锅</dd>
            <dd>火锅</dd>
            <dd>火锅</dd>
          </dl>
          <dl
            style="display:none"
            class="searchList">
            <dd>火锅</dd>
            <dd>火锅</dd>
            <dd>火锅</dd>
            <dd>火锅</dd>
          </dl>
        </div>
        <!-- 这里是搜索框正下方的推荐部分 -->
        <p class="suggest">
          <a href="#">故宫</a>
          <a href="#">故宫</a>
          <a href="#">故宫</a>
          <a href="#">故宫</a>
        </p>
        <ul class="nav">
          <li><nuxt-link
            to="/"
            class="takeout">美团外卖</nuxt-link></li>
          <li><nuxt-link
            to="/"
            class="movie">猫眼电影</nuxt-link></li>
          <li><nuxt-link
            to="/"
            class="hotel">美团酒店</nuxt-link></li>
          <li><nuxt-link
            to="/"
            class="apartment">民宿/公寓</nuxt-link></li>
          <li><nuxt-link
            to="/"
            class="business">商家入驻</nuxt-link></li>
        </ul>
      </el-col>
      <el-col
        :span="6"
        class="right">
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {};
</script>

<style lang="css">
</style>
