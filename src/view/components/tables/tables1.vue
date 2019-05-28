<template>
  <div>
    <Card>
      <Table border editable highlight-row :columns="columns" :data="data">
        <template slot-scope="{ row }" slot="name">
          <strong>{{ row.name }}</strong>
        </template>
        <template slot-scope="{ row, index }" slot="action">
          <Icon style="margin-right: 5px" type="md-add" size="16" @click="add(index)"/>
          <Icon style="margin-right: 5px" type="md-trash" size="16" @click="remove(index)"/>
          <Icon style="margin-right: 5px" type="md-create" size="16" @click="write(index)"/>
          <Icon type="md-eye" size="16" @click="read(index)"/>
        </template>
      </Table>
    </Card>
  </div>
</template>

<script>
// import { getTableData } from "@/api/data";
export default {
  name: "tables1",
  components: {},
  data() {
    return {
      columns: [
        {
          type: "selection",
          width: 60,
          align: "center"
        },
        {
          title: "Name",
          slot: "name"
        },
        {
          title: "Age",
          key: "age",
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
          title: "Address",
          key: "address",
          editable: true,
          filters: [
            {
              label: "New York",
              value: "New York"
            },
            {
              label: "London",
              value: "London"
            },
            {
              label: "Sydney",
              value: "Sydney"
            }
          ],
          filterMethod(value, row) {
            return row.address.indexOf(value) > -1;
          }
        },
        {
          title: "Action",
          slot: "action",
          width: 150,
          align: "center"
        }
      ],
      data: [
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
    add(index) {
      // console.log(index, this.data);
      this.data.splice(index + 1, 0, {});
    },
    remove(index) {
      this.data.splice(index, 1);
    },
    read(index) {
      this.$Modal.info({
        title: "User Info",
        content: `Name：${this.data[index].name}<br>Age：${
          this.data[index].age
        }<br>Address：${this.data[index].address}`
      });
    },
    write(index) {
      console.log(index, this.data);
    }
  },
  mounted() {}
};
</script>

<style lang="less">
i.ivu-icon {
  cursor: pointer;
}
</style>
