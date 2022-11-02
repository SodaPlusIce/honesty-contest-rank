<template>
  <div class="bgBackground">
    <Card :bordered="false">
      <template #title
        ><h1 style="padding: 10px">
          东南大学2022年诚信教育知识竞赛决赛排名
        </h1></template
      >
      <div>
        <Table
          ref="currentRowTable"
          size="large"
          :columns="columns"
          :data="data"
        ></Table>
      </div>
    </Card>
  </div>
</template>
<style>
.bgBackground {
  background: url(../static/poster.png);
  /* margin-top: 140px; */
  padding: 40px;
}
</style>
<script>
import bus from "@/utils";
import { onMounted } from "@vue/runtime-core";

export default {
  data() {
    return {
      columns: [
        {
          type: "index",
          width: 80,
          align: "center",
        },
        {
          title: "学院",
          width: 320,
          key: "name",
        },
        {
          title: "分数",
          key: "age",
        },
        // {
        //   title: "成员",
        //   key: "address",
        // },
      ],
      data: [
        {
          name: "经济管理学院",
          age: 110,
        },
        {
          name: "物理学院",
          age: 195,
        },
        // {
        //   name: "能源与环境学院",
        //   age: 110,
        // },
        // {
        //   name: "公共卫生学院",
        //   age: 110,
        // },
        //---------------分割线---------------------
        // {
        //   name: "材料科学与工程学院",
        //   age: 110,
        // },
        // {
        //   name: "数学学院",
        //   age: 90,
        // },
        {
          name: "四牌楼新生办",
          age: 185,
        },
        {
          name: "外国语学院",
          age: 190,
        },
      ],
    };
  },
  // setup() {
  //   onMounted(() => {
  //     bus.on("update", (val) => {
  //       // history.go(0);
  //       console.log("---------------");
  //       console.log(val);
  //       // this.data[val].age = window.localStorage.getItem(this.data[val].sm);
  //     });
  //   });
  // },
  mounted() {
    this.data.sort((a, b) => {
      return b.age - a.age;
    });
    // bus.on("update", (val) => {
    //   // history.go(0);
    //   console.log("---------------");
    //   console.log(val);
    //   this.data[val].age = window.localStorage.getItem(this.data[val].sm);
    // });
  },
  methods: {
    handleClearCurrentRow() {
      this.$refs.currentRowTable.clearCurrentRow();
    },
  },
};
</script>
