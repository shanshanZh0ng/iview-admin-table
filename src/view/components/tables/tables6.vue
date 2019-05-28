<template>
  <div>
    <Card>
      <h3>多功能表格</h3>
      <i-table border :columns="columns" :data="data"></i-table>
    </Card>
  </div>
</template>
<script>
import { utils } from "@/api/utils.js";
export default {
  name: "tables6",
  data() {
    return {
      data: [
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
          type: "aaa",
          datetime: "2019-5-20",
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
          type: "hhh",
          datetime: "2019-5-20",
          address: "北京",
          $isEdit: false
        }
      ],
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
      Types: [
        { value: "hhh", name: "hhh" },
        { value: "aaa", name: "aaa" },
        { value: "cccc", name: "cccc" },
        { value: "tytyty", name: "tytyty" }
      ]
    };
  },

  computed: {
    columns() {
      const _this = this;
      return [
        {
          title: "项目名称",
          titleHtml: '项目名称 <i class="ivu-icon ivu-icon-edit"></i>',
          editable: true,
          key: "name",
          align: "center",
          render: (h, params) => {
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
          title: "分类",
          key: "type",
          align: "center",
          render(h, { row, index }) {
            // console.log(row, index);
            if (row.$set) {
              return h(
                "Select",
                {
                  props: {
                    value: row.type,
                    transfer: true
                  },
                  on: {
                    "on-change": value => {
                      row.type = value;
                      _this.data[index] = row;
                    }
                  }
                },
                _this.Types.map(json => {
                  // console.log(json)
                  return h(
                    "Option",
                    {
                      props: {
                        value: json.value
                      }
                    },
                    json.name
                  );
                })
              );
            } else {
              return <div>{row.type}</div>;
            }
          }
        },
        {
          title: "数量",
          key: "age",
          align: "center",

          render: (h, params) => {
            //   params.row.$isEdit == params.column.key && params.row.$set

            if (params.row.$set) {
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
          title: "时间",
          key: "datetime",
          align: "center",
          width: 220,
          render(h, { row, index }) {
            // console.log(row, index);
            if (row.$set) {
              return h("DatePicker", {
                props: {
                  type: "datetime",
                  placeholder: "Select date",
                  transfer: true,
                  value: row.datetime,
                  format: "yyyy-MM-dd"
                },
                on: {
                  "on-change": function(date) {
                    row.datetime = date;
                  }
                }
              });
            } else {
              return <div>{row.datetime}</div>;
            }
          }
        },
        {
          align: "center",
          title: "地点",
          key: "address"
        },
        {
          align: "center",
          title: "操作",
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
                            this.data[index].name.list
                          }<br>年龄：${this.data[index].age}<br>地址：${
                            this.data[index].address
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
                        this.data.splice(index, 0, {
                          name: {
                            value: "",
                            list: this.listData
                          },
                          age: " ",
                          $isEdit: false
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
                        this.data.splice(index, 1);
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
      ];
    }
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
        type: "",
        address: "",
        $isEdit: false
      });
    }
  }
};
</script>
<style>
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
