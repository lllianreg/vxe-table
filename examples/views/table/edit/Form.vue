<template>
  <div>
    <p class="tip">表格与表单的组合使用</p>

    <vxe-form :data="formData" @submit="findList">
      <vxe-form-item title="app.body.label.name" field="name" :item-render="{}">
        <template #default="{ data }">
          <vxe-input v-model="data.name" placeholder="请输入名称"></vxe-input>
        </template>
      </vxe-form-item>
      <vxe-form-item title="性别" field="sex" :item-render="{}">
        <template #default="{ data }">
          <vxe-select v-model="data.sex" placeholder="请选择性别">
            <vxe-option v-for="(item, index) in sexList" :key="index" :value="item.value" :label="item.label"></vxe-option>
          </vxe-select>
        </template>
      </vxe-form-item>
      <vxe-form-item>
        <template #default>
          <vxe-button type="submit" status="primary">查询</vxe-button>
          <vxe-button type="reset">重置</vxe-button>
        </template>
      </vxe-form-item>
    </vxe-form>

    <vxe-table
      border
      resizable
      show-overflow
      :loading="loading"
      :data="tableData"
      :edit-config="{trigger: 'click', mode: 'cell'}">
      <vxe-column type="seq" width="60"></vxe-column>
      <vxe-column field="name" title="Name" :edit-render="{name: 'input', attrs: {type: 'text'}}"></vxe-column>
      <vxe-column field="role" title="Role" :edit-render="{name: 'input', attrs: {type: 'text'}}"></vxe-column>
      <vxe-column field="sex" title="Sex" :edit-render="{name: '$select', options: sexList}"></vxe-column>
      <vxe-column field="age" title="Age" :edit-render="{name: '$input', props: {type: 'number'}}"></vxe-column>
      <vxe-column field="date13" title="Date" :edit-render="{name: '$input', props: {type: 'date'}}"></vxe-column>
    </vxe-table>

    <p class="demo-code">{{ $t('app.body.button.showCode') }}</p>

    <pre>
      <pre-code class="xml">{{ demoCodes[0] }}</pre-code>
      <pre-code class="javascript">{{ demoCodes[1] }}</pre-code>
    </pre>
  </div>
</template>

<script>
export default {
  data () {
    return {
      loading: false,
      formData: {
        name: '',
        sex: ''
      },
      sexList: [
        { label: '女', value: '0' },
        { label: '男', value: '1' }
      ],
      tableData: [],
      demoCodes: [
        `
        <vxe-form :data="formData" @submit="findList">
          <vxe-form-item title="app.body.label.name" field="name" :item-render="{}">
            <template #default="{ data }">
              <vxe-input v-model="data.name" placeholder="请输入名称"></vxe-input>
            </template>
          </vxe-form-item>
          <vxe-form-item title="性别" field="sex" :item-render="{}">
            <template #default="{ data }">
              <vxe-select v-model="data.sex" placeholder="请选择性别">
                <vxe-option v-for="(item, index) in sexList" :key="index" :value="item.value" :label="item.label"></vxe-option>
              </vxe-select>
            </template>
          </vxe-form-item>
          <vxe-form-item>
            <template #default>
              <vxe-button type="submit" status="primary">查询</vxe-button>
              <vxe-button type="reset">重置</vxe-button>
            </template>
          </vxe-form-item>
        </vxe-form>

        <vxe-table
          border
          resizable
          show-overflow
          :loading="loading"
          :data="tableData"
          :edit-config="{trigger: 'click', mode: 'cell'}">
          <vxe-column type="seq" width="60"></vxe-column>
          <vxe-column field="name" title="Name" :edit-render="{name: 'input', attrs: {type: 'text'}}"></vxe-column>
          <vxe-column field="role" title="Role" :edit-render="{name: 'input', attrs: {type: 'text'}}"></vxe-column>
          <vxe-column field="sex" title="Sex" :edit-render="{name: '$select', options: sexList}"></vxe-column>
          <vxe-column field="age" title="Age" :edit-render="{name: '$input', props: {type: 'number'}}"></vxe-column>
          <vxe-column field="date13" title="Date" :edit-render="{name: '$input', props: {type: 'date'}}"></vxe-column>
        </vxe-table>
        `,
        `
        export default {
          data () {
            return {
              loading: false,
              formData: {
                name: '',
                sex: ''
              },
              sexList: [
                { label: '女', value: '0' },
                { label: '男', value: '1' }
              ],
              tableData: []
            }
          },
          created () {
            this.findList()
          },
          methods: {
            findList () {
              this.loading = true
              setTimeout(() => {
                this.loading = false
                this.tableData = [
                  { id: 10001, name: 'Test1', nickname: 'T1', role: 'Develop', sex: '0', sex2: ['0'], num1: 40, age: 28, address: 'Shenzhen', date12: '', date13: '' },
                  { id: 10002, name: 'Test2', nickname: 'T2', role: 'Designer', sex: '1', sex2: ['0', '1'], num1: 44, age: 22, address: 'Guangzhou', date12: '', date13: '2020-08-20' },
                  { id: 10003, name: 'Test3', nickname: 'T3', role: 'Test', sex: '0', sex2: ['1'], num1: 200, age: 32, address: 'Shanghai', date12: '2020-09-10', date13: '' },
                  { id: 10004, name: 'Test4', nickname: 'T4', role: 'Designer', sex: '1', sex2: ['1'], num1: 30, age: 23, address: 'Shenzhen', date12: '', date13: '2020-12-04' },
                  { id: 10005, name: 'Test5', nickname: 'T5', role: 'Develop', sex: '0', sex2: ['1', '0'], num1: 20, age: 30, address: 'Shanghai', date12: '2020-09-20', date13: '' },
                  { id: 10006, name: 'Test6', nickname: 'T6', role: 'Designer', sex: '1', sex2: ['0'], num1: 10, age: 21, address: 'Shenzhen', date12: '', date13: '' },
                  { id: 10007, name: 'Test7', nickname: 'T7', role: 'Develop', sex: '0', sex2: ['0'], num1: 5, age: 29, address: 'Shenzhen', date12: '2020-01-02', date13: '2020-09-20' },
                  { id: 10008, name: 'Test8', nickname: 'T8', role: 'PM', sex: '1', sex2: ['0'], num1: 2, age: 35, address: 'Shenzhen', date12: '', date13: '' }
                ]
              }, 300)
            }
          }
        }
        `
      ]
    }
  },
  created () {
    this.findList()
  },
  methods: {
    findList () {
      this.loading = true
      setTimeout(() => {
        this.loading = false
        this.tableData = [
          { id: 10001, name: 'Test1', nickname: 'T1', role: 'Develop', sex: '0', sex2: ['0'], num1: 40, age: 28, address: 'Shenzhen', date12: '', date13: '' },
          { id: 10002, name: 'Test2', nickname: 'T2', role: 'Designer', sex: '1', sex2: ['0', '1'], num1: 44, age: 22, address: 'Guangzhou', date12: '', date13: '2020-08-20' },
          { id: 10003, name: 'Test3', nickname: 'T3', role: 'Test', sex: '0', sex2: ['1'], num1: 200, age: 32, address: 'Shanghai', date12: '2020-09-10', date13: '' },
          { id: 10004, name: 'Test4', nickname: 'T4', role: 'Designer', sex: '1', sex2: ['1'], num1: 30, age: 23, address: 'Shenzhen', date12: '', date13: '2020-12-04' },
          { id: 10005, name: 'Test5', nickname: 'T5', role: 'Develop', sex: '0', sex2: ['1', '0'], num1: 20, age: 30, address: 'Shanghai', date12: '2020-09-20', date13: '' },
          { id: 10006, name: 'Test6', nickname: 'T6', role: 'Designer', sex: '1', sex2: ['0'], num1: 10, age: 21, address: 'Shenzhen', date12: '', date13: '' },
          { id: 10007, name: 'Test7', nickname: 'T7', role: 'Develop', sex: '0', sex2: ['0'], num1: 5, age: 29, address: 'Shenzhen', date12: '2020-01-02', date13: '2020-09-20' },
          { id: 10008, name: 'Test8', nickname: 'T8', role: 'PM', sex: '1', sex2: ['0'], num1: 2, age: 35, address: 'Shenzhen', date12: '', date13: '' }
        ]
      }, 300)
    }
  }
}
</script>
