<template>
  <div>
    <t-table rowKey="id" :columns="columns" :data="data" show-columns>
      <template #status="{ row }">
        <p v-if="row.status === 0" class="status">健康</p>
        <p v-if="row.status === 1" class="status unhealth">异常</p>
      </template>
      <template #op-column><p>操作</p></template>
      <template #op="slotProps">
        <a class="link" @click="rehandleClickOp(slotProps)">管理</a>
        <a class="link" @click="rehandleClickOp(slotProps)">删除</a>
      </template>
    </t-table>
  </div>
</template>

<script>
const columns = [
  { colKey: 'instance', title: '集群名称', width: 150 },
  {
    colKey: 'status',
    title: '状态',
    width: 100,
    cell: 'status',
  },
  { colKey: 'owner', title: '管理员' },
  { colKey: 'description', title: '描述' },
  {
    colKey: 'op',
    width: 200,
    title: 'op-column',
    cell: 'op',
  },
];
const data = [
  {
    id: 1,
    instance: 'JQTest1',
    status: 0,
    owner: 'jenny;peter',
    description: 'test',
  },
  {
    id: '2',
    instance: 'JQTest2',
    status: 1,
    owner: 'jenny',
    description: 'test',
  },
  {
    id: 3,
    instance: 'JQTest3',
    status: 0,
    owner: 'jenny',
    description: 'test',
  },
  {
    id: 4,
    instance: 'JQTest4',
    status: 1,
    owner: 'peter',
    description: 'test',
  },
];
export default {
  data() {
    return {
      columns,
      data,
    };
  },
  methods: {
    rehandleClickOp(data) {
      console.log(data);
    },
  },
};
</script>

<style lang="less" scoped>
/deep/ [class*='t-button'] .t-icon {
  background-color: transparent;
}
.link {
  cursor: pointer;
  margin-right: 15px;
}
.status {
  position: relative;
  color: #00a870;
  margin-left: 10px;
  &::before {
    position: absolute;
    top: 50%;
    left: 0;
    transform: translateY(-50%);
    content: '';
    background-color: #00a870;
    width: 6px;
    height: 6px;
    margin-left: -10px;
    border-radius: 50%;
  }
}
.status.unhealth {
  color: #e34d59;
  &::before {
    background-color: #e34d59;
  }
}
.more-detail {
  margin: 0 100px;
  > p {
    display: inline-block;
    margin: 5px;
  }
  > p.title {
    width: 100px;
  }
}
</style>
