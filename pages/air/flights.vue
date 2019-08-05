<template>
  <section class="contianer">
    <el-row type="flex"
            justify="space-between">

      <!-- 顶部过滤列表 -->
      <div class="flights-content">
        <!-- 过滤条件 -->
        <div>

        </div>

        <!-- 航班头部布局 -->
        <FlightsListHead />

        <!-- 航班信息 -->
        <div>
          <!-- 航班列表 -->
          <FlightsItem v-for="(item,index) in dataList"
                       :key="index"
                       :data="item" />

          <!-- 分页 -->
          <el-row type="flex"
                  justify="center"
                  style="margin-top:10px;">
            <!-- size-change：切换条数时候触发 -->
            <!-- current-change：选择页数时候触发 -->
            <!-- current-page: 当前页数 -->
            <!-- page-size：当前条数 -->
            <!-- total：总条数 -->
            <el-pagination @size-change="handleSizeChange"
                           @current-change="handleCurrentChange"
                           :current-page="pageIndex"
                           :page-sizes="[2, 4, 6, 8]"
                           :page-size="pageSize"
                           layout="total, sizes, prev, pager, next, jumper"
                           :total="total">
            </el-pagination>
          </el-row>
        </div>
      </div>

      <!-- 侧边栏 -->
      <div class="aside">
        <!-- 侧边栏组件 -->
      </div>
    </el-row>
  </section>
</template>

<script>

import moment from "moment";
import FlightsListHead from "@/components/air/flightsListHead.vue";
import FlightsItem from "@/components/air/flightsItem.vue"

export default {
  data () {
    return {
      dataList:[],
      pageIndex: 1, // 当前页数
      pageSize: 2,  // 显示条数
      total:0,
      // 后台返回的数据列表
      flightsData: {}
    }
  },
  components: {
    FlightsListHead,
    FlightsItem
  },
  methods:{
    // 修改分页条数pageSize的时候触发
    handleSizeChange(value){
      this.pageSize = value
      // 修改dataList的数据
      this.getDataList()
    },
    //切换页数pageIndex的时候触发
    handleCurrentChange(value){
      this.pageIndex = value
      // 修改dataList的数据
      this.getDataList()
    },
    // 获取分页的数据
    getDataList(){
      this.dataList = this.flightsData.flights.slice((this.pageIndex-1)*this.pageSize,this.pageIndex*this.pageSize)
    }
  },
  mounted () {
    //   console.log(this.$route.query);
    //请求数据列表
    this.$axios({
      url: "/airs",
      params: this.$route.query
    }).then(res => {
      // console.log(res.data);
      // 保存总的大数据
      this.flightsData = res.data
      //总条数
      this.total = this.flightsData.flights.length
      //切割当前页面要显示的数据
      this.dataList = this.flightsData.flights.slice(0,2)
    })
  }
}
</script>

<style scoped lang="less">
.contianer {
  width: 1000px;
  margin: 20px auto;
}

.flights-content {
  width: 745px;
  font-size: 14px;
}

.aside {
  width: 240px;
}
</style>