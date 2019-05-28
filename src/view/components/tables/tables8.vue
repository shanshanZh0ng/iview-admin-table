<template>
  <div>
    <Card height="600px">
      <Tabs value="name1">
        <TabPane label="标签一" name="name1">
          <i-table border :columns="columns" :data="showList"></i-table>
          <Page
            :total="dataCount"
            :page-size="pageSize"
            @on-change="changepage"
            show-total
            show-elevator
          />
          <div style="padding:10px;"></div>
          <i-table border :columns="columns1" :data="data1"></i-table>
        </TabPane>
        <TabPane label="标签二" name="name2">
          <Steps :current="1">
            <Step title="已完成" content="这里是该步骤的描述信息"></Step>
            <Step title="进行中" content="这里是该步骤的描述信息"></Step>
            <Step title="待进行" content="这里是该步骤的描述信息"></Step>
            <Step title="待进行" content="这里是该步骤的描述信息"></Step>
          </Steps>
          <div>
            <Slider v-model="s1"></Slider>
            <Slider v-model="s2" range></Slider>
            <Slider v-model="s3" range disabled></Slider>
          </div>
          <CellGroup>
            <Cell title="跳转标签" to="tables7">
              <Badge :count="10" slot="extra"/>
            </Cell>
          </CellGroup>
          <div style="padding:5px 0;">
            <Input v-model="value" placeholder="请输入..." style="width: 300px"/>
            <span style="margin-left:20px;">绑定信息展示：</span>
            <Input v-model="value" style="width: 300px"/>
            <Input
              search
              enter-button
              placeholder="Enter something..."
              style="width: 300px;float:left;margin-right:30px;"
            />
          </div>
          <RadioGroup v-model="phone">
            <Radio label="apple">
              <Icon type="logo-apple"></Icon>
              <span>Apple</span>
            </Radio>
            <Radio label="android">
              <Icon type="logo-android"></Icon>
              <span>Android</span>
            </Radio>
            <Radio label="windows">
              <Icon type="logo-windows"></Icon>
              <span>Windows</span>
            </Radio>
          </RadioGroup>
          <CheckboxGroup v-model="social">
            <Checkbox label="twitter">
              <Icon type="logo-twitter"></Icon>
              <span>Twitter</span>
            </Checkbox>
            <Checkbox label="facebook">
              <Icon type="logo-facebook"></Icon>
              <span>Facebook</span>
            </Checkbox>
            <Checkbox label="github">
              <Icon type="logo-github"></Icon>
              <span>Github</span>
            </Checkbox>
            <Checkbox label="snapchat">
              <Icon type="logo-snapchat"></Icon>
              <span>Snapchat</span>
            </Checkbox>
          </CheckboxGroup>
          <p v-model="social">
            <span>复选框选中的内容：</span>
            {{social}}
          </p>
          <Cascader :data="selectData" trigger="hover" style="width:500px;"></Cascader>
          <i-switch :model="switchValue" size="large">
            <span slot="open">On</span>
            <span slot="close">Off</span>
          </i-switch>
        </TabPane>
        <TabPane label="标签三" name="name3">
          <div>
            <Form :model="formItem" :label-width="80">
              <FormItem label="Input">
                <Input v-model="formItem.input" placeholder="Enter something..."></Input>
              </FormItem>
              <FormItem label="Select">
                <Select v-model="formItem.select">
                  <Option value="beijing">beijing</Option>
                  <Option value="shanghai">shanghai</Option>
                  <Option value="shenzhen">shenzhen</Option>
                </Select>
              </FormItem>
              <FormItem label="DatePicker">
                <Row>
                  <Col span="3">
                    <DatePicker type="date" placeholder="Select date" v-model="formItem.date"></DatePicker>
                  </Col>
                  <Col span="1" style="text-align: center">-</Col>
                  <Col span="3">
                    <TimePicker type="time" placeholder="Select time" v-model="formItem.time"></TimePicker>
                  </Col>
                </Row>
              </FormItem>
              <FormItem label="Radio">
                <RadioGroup v-model="formItem.radio">
                  <Radio label="male">Male</Radio>
                  <Radio label="female">Female</Radio>
                </RadioGroup>
              </FormItem>
              <FormItem label="Checkbox">
                <CheckboxGroup v-model="formItem.checkbox">
                  <Checkbox label="Eat"></Checkbox>
                  <Checkbox label="Sleep"></Checkbox>
                  <Checkbox label="Run"></Checkbox>
                  <Checkbox label="Movie"></Checkbox>
                </CheckboxGroup>
              </FormItem>
              <FormItem label="Switch">
                <i-switch v-model="formItem.switch" size="large">
                  <span slot="open">On</span>
                  <span slot="close">Off</span>
                </i-switch>
              </FormItem>
              <FormItem label="Slider">
                <Slider v-model="formItem.slider" range></Slider>
              </FormItem>
              <FormItem label="Text">
                <Input
                  v-model="formItem.textarea"
                  type="textarea"
                  :autosize="{minRows: 2,maxRows: 5}"
                  placeholder="Enter something..."
                ></Input>
              </FormItem>
              <FormItem>
                <Button type="primary" @click="sunbmit()">Submit</Button>
                <Button style="margin-left: 8px">Cancel</Button>
              </FormItem>
            </Form>
          </div>
        </TabPane>
      </Tabs>
    </Card>
  </div>
</template>
<script>
let _ = require("lodash");
// import _ form "lodash";
export default {
  name: "tables8",
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
          name: "大数据1",
          num: 18,
          type: "边缘计算",
          datetime: "2019-5-20",
          address: "上海"
        },
        {
          name: "人工智能1",
          num: 24,
          type: "区块链",
          datetime: "2019-5-21",
          address: "北京"
        },
        {
          name: "测试",
          num: 18,
          type: "随便",
          datetime: "2019-5-20",
          address: "上海"
        },
        {
          name: "大数据2",
          num: 18,
          type: "边缘计算",
          datetime: "2019-5-20",
          address: "上海"
        },
        {
          name: "人工智能2",
          num: 24,
          type: "区块链",
          datetime: "2019-5-21",
          address: "北京"
        }
      ],
      change: false,
      showList: [],
      dataCount: 0,
      pageSize: 2,
      //第二个
      s1: 30,
      s2: [20, 45],
      s3: [10, 50],
      value: "",
      phone: "apple",
      social: ["facebook", "github"],
      selectData: [
        {
          value: "beijing",
          label: "北京",
          children: [
            {
              value: "gugong",
              label: "故宫"
            },
            {
              value: "tiantan",
              label: "天坛"
            },
            {
              value: "wangfujing",
              label: "王府井"
            }
          ]
        },
        {
          value: "jiangsu",
          label: "江苏",
          children: [
            {
              value: "nanjing",
              label: "南京",
              children: [
                {
                  value: "fuzimiao",
                  label: "夫子庙"
                }
              ]
            },
            {
              value: "suzhou",
              label: "苏州",
              children: [
                {
                  value: "zhuozhengyuan",
                  label: "拙政园"
                },
                {
                  value: "shizilin",
                  label: "狮子林"
                }
              ]
            }
          ]
        }
      ],
      switchValue: true,
      //第三个
      formItem: {
        input: "",
        select: "",
        radio: "male",
        checkbox: [],
        switch: true,
        date: "",
        time: "",
        slider: [20, 50],
        textarea: ""
      },
      data1: [
        { id: 1, treatment: 1, state: "已处理" },
        { id: 2, treatment: 1, state: "已处理" },
        { id: 3, treatment: 0, state: "未处理" }
      ]
    };
  },
  computed: {
    columns() {
      const _this = this;
      //   _this.dataCount = _this.data.legnth;
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
                          content: `${'<i-table border :columns="columns" :data="data"></i-table>'}`
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
    },
    columns1() {
      const _this = this;
      return [
        {
          title: "状态",
          key: "state",
          align: "center"
        },
        {
          fixed: "right",
          title: "Action",
          key: "action",
          width: 250,
          align: "center",
          render: (h, params) => {
            return h("div", [
              h(
                "strong",
                {
                  style: {
                    marginRight: "5px"
                  }
                },
                params.row.state
              ),
              h("i-switch", {
                //数据库1是已处理，0是未处理
                props: {
                  type: "primary",
                  value: params.row.treatment === 1 //控制开关的打开或关闭状态，官网文档属性是value
                },
                style: {
                  marginRight: "5px"
                },
                on: {
                  "on-change": value => {
                    //触发事件是on-change,用双引号括起来，
                    //参数value是回调值，并没有使用到
                    this.switch(params.index); //params.index是拿到table的行序列，可以取到对应的表格值
                  }
                }
              })
            ]);
          }
        }
      ];
    }
  },
  methods: {
    inChan() {
      let object = { a: 1 };
      let other = { a: 1 };
      _.isEqual(object, other);
    },

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
    },
    changepage(index) {
      var _start = (index - 1) * this.pageSize;
      var _end = index * this.pageSize;
      this.showList = this.data.slice(_start, _end);
    },
    //表格开关
    switch(index) {
      //打开是true,已经处理1
      if (this.data1[index].treatment === 1) {
        this.data1[index].treatment = 0;
        this.updateFeedbackMessage(
          this.data1[index].id,
          "treatment",
          this.data1[index].treatment
        );
      } else {
        this.updateFeedbackMessage(this.data1[index].id, "treatment", 1);
      }
    },
    //更新反馈信息某一字段
    updateFeedbackMessage(id, key, value) {
      this.data1.forEach((item, index) => {
        if (item.id === id) {
          item[key] = value;
          item.state = Boolean(value) ? "已处理" : "未处理";
        }
      });
      this.$Message.success("状态修改成功");
    },
    sunbmit() {
      console.log(this.formItem);
    }
  },
  mounted() {
    let object = { a: 1, b: 2 };
    let other = { a: 1 };
    console.log(_.isEqual(object, other));
    this.dataCount = this.data.length;
    if (this.dataCount < this.pageSize) {
      this.showList = this.data;
    } else {
      this.showList = this.data.slice(0, this.pageSize);
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
.ivu-page {
  text-align: right;
}
</style>
