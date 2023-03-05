<template>
  <div>
    <el-container>
      <el-header>
        <div>
          <!-- 页面眉头 -->
          <el-row>
            <!-- 公司名称，可跳转首页 -->
            <el-col :span="5" style="height: 60px"
              ><div class="center">
                {{ HomeData.CompanyName }}
              </div></el-col
            >
            <!-- 各分页面 -->
            <el-col :span="8" :offset="5">
              <el-menu
                text-color="black"
                background-color="white"
                mode="horizontal"
                :unique-opened="true"
                :router="true"
              >
                <el-menu-item
                  v-for="item in HomeData.CompanyInf"
                  :key="item.id"
                  style="font-size: 18px"
                >
                  {{ item }}
                </el-menu-item>
              </el-menu>
            </el-col>
            <!-- 搜索 -->
            <el-col :span="1" style="height: 60px">
              <div class="center">
                <i class="el-icon-search"></i>
              </div>
            </el-col>
            <!-- 咨询按钮 -->
            <el-col :span="5" style="height: 60px"
              ><div style="display: flex; align-items: center; height: 100%">
                <el-button type="primary" icon="el-icon-search">{{
                  HomeData.Consultas
                }}</el-button>
              </div></el-col
            >
          </el-row>
        </div>
      </el-header>
      <el-main>
        <!-- 轮播图 -->
        <div>
          <el-carousel :interval="4000" arrow="never">
            <el-carousel-item
              v-for="(image, index) in SwiperImages"
              :key="index"
            >
              <img :src="image" alt="carousel image" />
            </el-carousel-item>
          </el-carousel>
        </div>
      </el-main>
      <el-footer>Footer</el-footer>
    </el-container>
  </div>
</template>

<script>
import HomeData from "@/Project/Projiect1/Home.json";
export default {
  data() {
    return {
      // 主页文字
      HomeData: HomeData,
      // 轮播图
      SwiperImages: [],
    };
  },
  mounted() {
    this.getSwiperImages();
  },
  methods: {
    // 获取文件夹中轮播图并存入数组
    getSwiperImages() {
      const files = require.context(
        "@/Project/Projiect1/",
        false,
        /\.(jpg|jpeg|png|gif)$/
      );
      files.keys().forEach((key) => {
        this.SwiperImages.push(files(key));
      });
    },
  },
};
</script>

<style lang="less" scoped>
// 居中样式
.center {
  display: flex;
  height: 100%;
  align-items: center;
  justify-content: center;
  font-size: 24px;
}

.el-menu {
  display: flex;
  justify-content: space-between;
}
.el-menu.el-menu--horizontal {
  border-bottom: 0;
}
.el-carousel {
  width: 1418px;
  height: 532px;
}
.el-carousel__item {
  width: 1418px;
  height: 532px;
}
.el-carousel__item img {
  object-fit: cover;
  width: 100%;
  height: 100%;
}
</style>