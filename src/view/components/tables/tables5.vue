<template>
  <div>
    <Card>
      <!-- <div class="port_head">
        <ul>
          <li>接口关系</li>
        </ul>
        <div class="port_head_right">
          <Button type="primary" class="prot_system_head_btn" @click="add">新增</Button>
          <Button type="primary" class="prot_system_head_btn">保存</Button>
        </div>
      </div>-->
      <h3>功能表格</h3>
      <i-table border :columns="columns2" :data="data3"></i-table>
    </Card>
  </div>
</template>
<script>
// import tables from "_c/tables";

export default {
  name: "tables5",
  data() {
    return {
      listData: [
        {
          value: 0,
          name: "西门子"
        },
        {
          value: 1,
          name: "华为"
        }
      ],
      columns2: [
        {
          title: "Name",
          key: "name",
          align: "center",
          render: (h, params) => {
            // console.log(params);
            if (params.row.$isEdit == params.column.key && params.row.$set) {
              return h(
                "Select",
                {
                  props: {
                    value: params.row.name.value,
                    transfer: true
                  },
                  on: {
                    "on-change": event => {
                      params.row.name.value = event;
                      this.$set(params.row, "$isEdit", -1);
                    }
                  }
                },
                params.row.name.list.map(item => {
                  return h("Option", {
                    props: {
                      value: item.value,
                      label: item.name
                    }
                  });
                })
              );
            } else {
              return h(
                "div",
                {
                  on: {
                    click: () => {
                      this.$set(params.row, "$isEdit", params.column.key);
                    }
                  }
                },
                params.row.name.list.map(item => {
                  return item.value == params.row.name.value ? item.name : null;
                })
              );
            }
          }
        },
        {
          title: "Age",
          key: "age",
          align: "center",

          render: (h, params) => {
            if (params.row.$isEdit == params.column.key && params.row.$set) {
              return h("Input", {
                props: {
                  type: "text",
                  value: params.row.age
                },

                on: {
                  "on-blur": event => {
                    params.row.age = event.target.value;
                    this.$set(params.row, "$isEdit", "");
                  }
                }
              });
            } else {
              return h(
                "div",
                {
                  on: {
                    click: () => {
                      this.$set(params.row, "$isEdit", params.column.key);
                    }
                  }
                },
                params.row.age
              );
            }
          }
        },
        {
          align: "center",
          title: "Address",
          key: "address"
        },
        {
          align: "center",
          title: "Action",
          key: "action",
          render: (h, params) => {
            return (
              "div",
              [
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
                        if (params.row.$set) {
                          this.handleSave(params.row);
                        } else {
                          this.handleEdit(params.row);
                        }
                      }
                    }
                  },
                  params.row.$set ? "保存" : "编辑"
                ),
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
                            this.data3[index].name.list
                          }<br>年龄：${this.data3[index].age}<br>地址：${
                            this.data3[index].address
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
                        // console.log(params);
                        let index = Number(params.index) + 1;
                        this.data3.splice(index, 0, {
                          name: {
                            value: "",
                            list: this.listData
                          }
                        });
                      }
                    }
                  },
                  "增加"
                ),
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
                        let index = params.index;
                        this.data3.splice(index, 1);
                        this.$Message.success("删除成功");
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
              ]
            );
          }
        }
      ],
      data3: [
        {
          name: {
            value: 0,
            list: [
              {
                value: 0,
                name: "西门子"
              },
              {
                value: 1,
                name: "华为"
              }
            ]
          },
          age: 18,
          address: "上海",
          $isEdit: false
        },
        {
          name: {
            value: 1,
            list: [
              {
                value: 0,
                name: "西门子"
              },
              {
                value: 1,
                name: "华为"
              }
            ]
          },
          age: 24,
          address: "北京",
          $isEdit: false
        }
      ]
    };
  },
  methods: {
    handleEdit(row) {
      this.$set(row, "$set", true);
    },
    handleSave(row) {
      this.$set(row, "$set", false);
      this.$set(row, "$isEdit", "");
      this.$Message.success("保存完成");
    },
    add() {
      this.data3.push({
        name: {
          value: "",
          list: this.listData
        },
        age: "",
        address: "",
        $isEdit: false
      });
    }
  }
};
</script>
<style>
/* @import "../../assets/css/head.css"; */
.ivu-table-wrapper {
  margin-top: 20px;
}
.ivu-table td,
.ivu-table th {
  height: 32px;
}

.ivu-input {
  height: 30px;
}
.ivu-table-cell {
  padding-left: 2px;
  padding-right: 2px;
}
</style>
