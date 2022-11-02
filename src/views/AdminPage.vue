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
        >
          <template #name="{ row }">
            <strong>{{ row.name }}</strong>
          </template>
          <template #action="{ index }">
            <Button type="primary" style="margin-right: 5px" @click="add(index)"
              >加10分</Button
            >
            <Button type="error" @click="sub(index)">减10分</Button>
          </template>
        </Table>
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
          title: "Name",
          slot: "name",
        },
        // {
        //   title: "学院",
        //   width: 320,
        //   key: "name",
        // },
        {
          title: "分数",
          key: "age",
        },
        // {
        //   title: "成员",
        //   key: "address",
        // },
        {
          title: "Action",
          slot: "action",
          align: "center",
        },
      ],
      data: [
        {
          name: "经济管理学院",
          sm: "jingguan",
          // age: window.localStorage.getItem("jingguan"),
          age: 0,
          address: "黄好，帅璐颖，吴思颉，孙小雯",
        },
        {
          name: "物理学院",
          sm: "wuli",
          // age: window.localStorage.getItem("wuli"),
          age: 0,
          address: "张万涛，杨艺天，李嘉淇，朱福军",
        },
        {
          name: "能源与环境学院",
          sm: "nenghuan",
          // age: window.localStorage.getItem("nenghuan"),
          age: 0,
          address: "夏侯桂芳，张秀颖，韦静，马怿铭",
        },
        {
          name: "公共卫生学院",
          sm: "gongwei",
          // age: window.localStorage.getItem("gongwei"),
          age: 0,
          address: "吴晶莹，龙瑞，卞彦文，张丕羽",
        },
        //---------------分割线---------------------
        {
          name: "材料科学与工程学院",
          sm: "cailiao",
          // age: window.localStorage.getItem("cailiao"),
          age: 0,
          address: "陈子霖，钟革萍，刘向锋，王雨彤",
        },
        {
          name: "数学学院",
          sm: "shuxue",
          // age: window.localStorage.getItem("shuxue"),
          age: 0,
          address: "姜修博，蒋卓然，李欣然，闫宇骁",
        },
        {
          name: "四牌楼新生办",
          sm: "sipailou",
          // age: window.localStorage.getItem("sipailou"),
          age: 0,
          address: "邵熙尧，孟子涵，赵佳艺，张津钰",
        },
        {
          name: "外国语学院",
          sm: "waiguoyu",
          // age: window.localStorage.getItem("waiguoyu"),
          age: 0,
          address: "陈小宇，李睿洋，刘昕彤，余枫英",
        },
      ],
    };
  },
  mounted() {
    window.localStorage.setItem("jingguan", 0);
    window.localStorage.setItem("wuli", 0);
    window.localStorage.setItem("nenghuan", 0);
    window.localStorage.setItem("gongwei", 0);
    window.localStorage.setItem("cailiao", 0);
    window.localStorage.setItem("shuxue", 0);
    window.localStorage.setItem("sipailou", 0);
    window.localStorage.setItem("waiguoyu", 0);
    this.data.sort((a, b) => {
      return b.age - a.age;
    });
  },
  methods: {
    handleClearCurrentRow() {
      this.$refs.currentRowTable.clearCurrentRow();
    },
    add(index) {
      window.localStorage.setItem(
        this.data[index].sm,
        window.localStorage.getItem(this.data[index].sm) - "0" + 10
      );
      this.data[index].age = window.localStorage.getItem(this.data[index].sm);
      bus.emit("update", index);
      this.data.sort((a, b) => {
        return b.age - a.age;
      });
    },
    sub(index) {
      window.localStorage.setItem(
        this.data[index].sm,
        window.localStorage.getItem(this.data[index].sm) - "0" - 10
      );
      this.data[index].age = window.localStorage.getItem(this.data[index].sm);
      bus.emit("update", index);
      this.data.sort((a, b) => {
        return b.age - a.age;
      });
    },
  },
};
</script>
