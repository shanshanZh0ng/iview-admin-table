<template>
  <div>
    <Card>
      <h3>多功能表格7</h3>
      <i-table border :columns="columns" :data="data"></i-table>
    </Card>
  </div>
</template>
<script>
export default {
  name: "tables7",
  data() {
    return {
      Types: [
        { value: "边缘计算", name: "边缘计算" },
        { value: "数据处理", name: "数据处理" },
        { value: "区块链", name: "区块链" },
        { value: "大数据展示", name: "大数据展示" }
      ],
      data: [
        {
          name: "大数据",
          num: 18,
          type: "边缘计算",
          datetime: "2019-5-20",
          address: "上海"
        },
        {
          name: "人工智能",
          num: 24,
          type: "区块链",
          datetime: "2019-5-21",
          address: "北京"
        },
        {
          name: "大数据",
          num: 18,
          type: "边缘计算",
          datetime: "2019-5-20",
          address: "上海"
        },
        {
          name: "人工智能",
          num: 24,
          type: "区块链",
          datetime: "2019-5-21",
          address: "北京"
        }
      ],
      change: false
    };
  },
  computed: {
    columns() {
      const _this = this;
      return [
        {
          title: "项目名称",
          key: "name",
          align: "center",
          render(h, { row, index }) {
            if (row.$set) {
              return h("Input", {
                props: {
                  size: "small",
                  value: row.name
                },
                on: {
                  input: event => {
                    if (row.name === event) {
                      _this.change = _this.change || false;
                    } else {
                      _this.change = _this.change || true;
                    }
                    row.name = event;
                    _this.data[index] = row;
                  }
                }
              });
            } else {
              return <div>{row.name}</div>;
            }
          }
        },
        {
          title: "分类",
          key: "type",
          align: "center",
          render(h, { row, index }) {
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
                      if (row.type === value) {
                        _this.change = _this.change || false;
                      } else {
                        _this.change = _this.change || true;
                      }
                      row.type = value;
                      _this.data[index] = row;
                    }
                  }
                },
                _this.Types.map(json => {
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
          key: "num",
          align: "center",
          render(h, { row, index }) {
            if (row.$set) {
              return h("Input", {
                props: {
                  size: "small",
                  value: row.num
                },
                on: {
                  input: event => {
                    if (row.num === event) {
                      _this.change = _this.change || false;
                    } else {
                      _this.change = _this.change || true;
                    }
                    row.num = event;
                    _this.data[index] = row;
                  }
                }
              });
            } else {
              return <div>{row.num}</div>;
            }
          }
        },
        {
          title: "时间",
          key: "datetime",
          align: "center",
          width: 220,
          render(h, { row, index }) {
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
                    // console.log(row.datetime, date);
                    if (row.datetime === date) {
                      _this.change = _this.change || false;
                    } else {
                      _this.change = _this.change || true;
                    }
                    row.datetime = date;
                    _this.data[index] = row;
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
          key: "address",
          render(h, { row, index }) {
            if (row.$set) {
              return h("Input", {
                props: {
                  size: "small",
                  value: row.address
                },
                on: {
                  input: event => {
                    if (row.address === event) {
                      _this.change = _this.change || false;
                    } else {
                      _this.change = _this.change || true;
                    }
                    row.address = event;
                    _this.data[index] = row;
                  }
                }
              });
            } else {
              return <div>{row.address}</div>;
            }
          }
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
                        let row = params.row;
                        let index = params.index;
                        // console.log(_this.data);
                        _this.$Modal.info({
                          title: "具体信息",
                          content: `项目名称：${
                            _this.data[index].name
                          }<br>分类：${_this.data[index].type}<br>数量：${
                            _this.data[index].num
                          }<br>时间：${_this.data[index].datetime}<br>地点：${
                            _this.data[index].address
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
                        let index = Number(params.index) + 1;
                        this.data.splice(index, 0, {
                          //   $isEdit: false
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
                            console.log(params);
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
      //   this.$set(row, "$isEdit", "");
      if (this.change) {
        this.$Message.success("保存完成");
      }
      this.change = false;
    }
  }
};
</script>
<style>
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
