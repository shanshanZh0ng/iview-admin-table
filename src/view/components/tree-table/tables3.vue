<template>
  <div>
    <Card>
      <h3>菜单列表</h3>
      <tree-table
        border
        stripe
        height="600"
        searchable
        search-place="top"
        expand-key="name"
        :expand-type="false"
        :selectable="false"
        :columns="columns"
        :data="data"
      >
        <template slot="state" slot-scope="scope">
          <Button :class="changeClass(scope)" @click="handle(scope)">{{scope.row.state}}</Button>
        </template>
      </tree-table>
    </Card>
  </div>
</template>

<script>
export default {
  name: "tables3",
  data() {
    return {
      columns: [
        {
          title: "菜单顺序码",
          key: "cguid",
          width: "90px",
          align: "center",
          headerAlign: "center"
        },
        {
          title: "菜单名称",
          key: "name",
          width: "300px",
          headerAlign: "center",
          headerAlign: "center"
        },
        {
          title: "菜单编码",
          key: "code",
          // width: "400px",
          align: "center",
          headerAlign: "center"
        },
        {
          title: "菜单说明",
          key: "explain",
          align: "center",
          headerAlign: "center"
        },
        {
          title: "链接路径",
          key: "path",
          // width: "400px",
          minWidth: "200px",
          align: "center",
          headerAlign: "center"
        },
        {
          title: "状态",
          key: "state",
          type: "template",
          template: "state",
          align: "center",
          headerAlign: "center"
        }
      ],
      data: [
        {
          cguid: 1,
          name: "订单管理",
          code: "mn1300",
          explain: "销售管理",
          path: "/scm/businessProcessController/toBusinessProcess.ht",
          state: "已启用",
          children: [
            {
              cguid: "0101",
              name: "生产订单",
              code: "SCDD_HIPAD",
              explain: "销售订单_海派",
              path: "/sa/salesOrderController/toSalesOrderelList.ht",
              state: "已启用"
            },
            {
              cguid: "0102",
              name: "计划订单",
              code: "JHDD",
              explain: "计划订单",
              path: "/aps/SAPPlanOrder/to_SAPPlanOrder_list.ht",
              state: "已启用"
            },
            {
              cguid: "0103",
              name: "销售订单_电器",
              code: "XSDD_HTDQ",
              explain: "销售订单_电器",
              path: "/sa/salesOrderController/toSalesOrderListae.ht",
              state: "已启用"
            }
          ]
        },
        {
          cguid: 2,
          name: "有限产能排产",
          code: "7bd2a0fd04c4483c939ae129c7c1f29a",
          explain: "有限产能排产",
          path: "无",
          state: "已禁用",
          children: [
            {
              cguid: "0201",
              name: "计划排产",
              code: "04c8c31c5d2444afa8a03157ce0590fe",
              explain: "计划排产",
              path: "/aps/apshomgen/tolisthomogen.ht",
              state: "已启用",
              children: [
                {
                  cguid: "020101",
                  name: "计划排产",
                  code: "04c8c31c5d2444afa8a03157ce0590fe",
                  explain: "计划排产",
                  path: "/aps/apshomgen/tolisthomogen.ht",
                  state: "已禁用"
                }
              ]
            },
            {
              cguid: "0202",
              name: "排产结果查看",
              code: "0849198971244661ac2e9545373e8852",
              explain: "排产结果查看",
              path: "/able/schedu/gante.ht",
              state: "已启用"
            }
          ]
        },
        {
          cguid: 3,
          name: "有限产能排产",
          code: "7bd2a0fd04c4483c939ae129c7c1f29a",
          explain: "有限产能排产",
          path: "无",
          state: "已禁用"
        },
        {
          cguid: 4,
          name: "有限产能排产",
          code: "7bd2a0fd04c4483c939ae129c7c1f29a",
          explain: "有限产能排产",
          path: "无",
          state: "已禁用",
          children: [
            {
              cguid: "0401",
              name: "有限产能排产",
              code: "7bd2a0fd04c4483c939ae129c7c1f29a",
              explain: "有限产能排产",
              path: "无",
              state: "已禁用"
            },
            {
              cguid: "0402",
              name: "有限产能排产",
              code: "7bd2a0fd04c4483c939ae129c7c1f29a",
              explain: "有限产能排产",
              path: "无",
              state: "已禁用"
            }
          ]
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
    }
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
