<template>
  <div>
    <Card>
      <h3>等级列表</h3>
      <Table border editable stripe highlight-row :columns="columns" :data="data">
        <template slot-scope="{ row }" slot="name">
          <strong>{{ row.name }}</strong>
        </template>
        <template slot="action">
          <Icon type="md-hammer" size="16" @click="ahref()"/>
        </template>
        <template slot="state" slot-scope="scope">
          <Button :class="changeClass(scope)" @click="handle(scope)">{{scope.row.state}}</Button>
        </template>
      </Table>
    </Card>
  </div>
</template>

<script>
// import { getTableData } from "@/api/data";
export default {
  name: "tables4",
  components: {},
  data() {
    return {
      columns: [
        {
          type: "index",
          width: 60,
          align: "center"
        },
        {
          title: "等级名称",
          key: "name",
          align: "center"
        },
        {
          title: "等级说明",
          key: "explain",
          align: "center"
        },
        {
          title: "等级图标",
          key: "icon",
          align: "center",
          render: (h, params) => {
            return h("Avatar", {
              props: {
                src: params.row.icon
              }
            });
          }
        },
        {
          title: "状态",
          slot: "state",
          align: "center"
        },
        {
          title: "操作",
          slot: "action",
          width: 150,
          align: "center"
        }
      ],
      data: [
        {
          name: "A级",
          explain: "123",
          icon: "https://i.loli.net/2017/08/21/599a521472424.jpg",
          state: "已启用"
        },
        {
          name: "B级",
          explain: "123",
          icon: "https://i.loli.net/2017/08/21/599a521472424.jpg",
          state: "已禁用"
        },
        {
          name: "A级",
          explain: "123",
          icon: "https://i.loli.net/2017/08/21/599a521472424.jpg",
          state: "已启用"
        },
        {
          name: "A级",
          explain: "123",
          icon: "https://i.loli.net/2017/08/21/599a521472424.jpg",
          state: "已启用"
        }
      ]
    };
  },
  methods: {
    handle(scope) {
      let state = scope.row.state;
      if (state === "已禁用") {
        scope.row.state = "已启用";
      } else {
        scope.row.state = "已禁用";
      }
    },
    changeClass(scope) {
      let state = scope.row.state;
      if (state === "已禁用") {
        return "gray";
      } else if (state === "已启用") {
        return "green";
      }
    },
    ahref() {
      //   location.href = "index.vue";
    }
  },
  mounted() {
    // getTableData().then(res => {
    //   console.log(res);
    //   //   this.tableData = res.data;
    // });
  }
};
</script>

<style lang="less">
.gray {
  background: gray;
  color: #fff;
}
.green {
  background: green;
  color: #fff;
}
</style>
