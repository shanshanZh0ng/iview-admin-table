<template>
  <tables
    ref="tables"
    border
    stripe
    height="600"
    highlight-row
    editable
    search-place="top"
    v-model="tableData"
    :columns="columns"
  />
</template>

<script>
import Tables from "_c/tables";
// import { getTableData } from "@/api/data";
export default {
  name: "tables2",
  components: {
    Tables
  },
  data() {
    return {
      columns: [
        {
          title: "姓名",
          key: "name",
          sortable: true,
          editable: false,
          render: (h, params) => {
            //console.log(params);
            return h("div", [
              h("Icon", {
                props: {
                  type: "person"
                }
              }),
              h("strong", params.row.name)
            ]);
          }
        },
        {
          title: "年龄",
          key: "age",
          editable: true,
          filters: [
            {
              label: "> 25",
              value: 1
            },
            {
              label: "< 25",
              value: 2
            }
          ],
          filterMultiple: false,
          filterMethod(value, row) {
            if (value === 1) {
              return row.age > 25;
            } else if (value === 2) {
              return row.age < 25;
            }
          }
        },
        {
          title: "地址",
          key: "address",
          editable: true,
          render: (h, params) => {
            console.log(params);
          }
        },
        {
          title: "操作",
          key: "action",
          align: "center",
          render: (h, params) => {
            // console.log(params);
            return h("div", [
              h(
                "Button",
                {
                  props: {
                    type: "info",
                    size: "small"
                  },
                  style: {
                    marginRight: "5px"
                  },
                  on: {
                    click: () => {
                      // console.log(h, params);
                      let row = params.row;
                      let index = params.index;
                      this.$Modal.info({
                        title: "具体信息",
                        content: `姓名：${
                          this.tableData[index].name
                        }<br>年龄：${this.tableData[index].age}<br>地址：${
                          this.tableData[index].address
                        }`
                      });
                    }
                  }
                },
                "查看"
              ),
              h(
                "Button",
                {
                  props: {
                    type: "success",
                    size: "small"
                  },
                  style: {
                    marginRight: "5px"
                  },
                  on: {
                    click: () => {
                      this.tableData.splice(params.index + 1, 0, {});
                    }
                  }
                },
                "增加"
              ),
              h(
                "Button",
                {
                  props: {
                    type: "primary",
                    size: "small"
                  },
                  style: {
                    marginRight: "5px"
                  },
                  on: {
                    click: () => {
                      console.log(this.names, params);
                    }
                  }
                },
                "修改"
              ),
              //弹窗层-包含按钮
              h(
                "Poptip",
                {
                  props: {
                    //这个参数很重要，影响到是否被遮挡的问题
                    transfer: true,
                    // placement: 'bottom',
                    confirm: true,
                    title: "你确定要删除吗?"
                  },
                  on: {
                    "on-ok": () => {
                      console.log(" 点击了确定删除！！！！", h, params);
                      let index = params.index;
                      this.tableData.splice(index, 1);
                    }
                  }
                },
                [
                  h(
                    "Button",
                    {
                      props: {
                        type: "error",
                        size: "small"
                      },
                      on: {
                        click: () => {
                          // this.deleteUser(params.row.USER_ID)
                        }
                      }
                    },
                    "删除"
                  )
                ]
              )
            ]);
          }
        }
      ],
      tableData: [
        {
          name: "John Brown",
          age: 18,
          address: "New York No. 1 Lake Park"
        },
        {
          name: "Jim Green",
          age: 24,
          address: "London No. 1 Lake Park"
        },
        {
          name: "Joe Black",
          age: 30,
          address: "Sydney No. 1 Lake Park"
        },
        {
          name: "Jon Snow",
          age: 26,
          address: "Ottawa No. 2 Lake Park"
        }
      ]
    };
  },
  methods: {
    // handleDelete(params) {
    //   console.log(params);
    // }
    // exportExcel() {
    //   this.$refs.tables.exportCsv({
    //     filename: `table-${new Date().valueOf()}.csv`
    //   });
    // }
  }
  //   mounted() {
  //     getTableData().then(res => {
  //       //   this.tableData = res.data;
  //     });
  //   }
};
</script>

<style>
/* .ivu-table-wrapper {
  overflow: inherit;
} */
</style>
