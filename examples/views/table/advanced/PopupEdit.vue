<template>
  <div>
    <p class="tip">实现弹框表单编辑功能<span class="red">（具体请自行实现，该示例仅供参考）</span></p>

    <vxe-table
      border
      resizable
      highlight-hover-row
      highlight-current-row
      height="500"
      :data="tableData">
      <vxe-column type="seq" width="60"></vxe-column>
      <vxe-column field="name" title="Name"></vxe-column>
      <vxe-column field="sex" title="Sex" :formatter="formatterSex"></vxe-column>
      <vxe-column field="age" title="Age"></vxe-column>
      <vxe-column field="address" title="Address" show-overflow></vxe-column>
      <vxe-column title="操作" width="100" show-overflow>
        <template #default="{ row }">
          <vxe-button type="text" icon="fa fa-edit" @click="editEvent(row)"></vxe-button>
          <vxe-button type="text" icon="fa fa-trash-o"></vxe-button>
        </template>
      </vxe-column>
    </vxe-table>

    <vxe-modal ref="xModal" v-model="showEdit" title="编辑&保存" width="800" resize destroy-on-close>
      <template #default>
        <vxe-form :data="formData" :rules="formRules" title-align="right" title-width="100" @submit="submitEvent">
          <vxe-form-item title="Basic information" span="24" title-align="left" title-width="200px" :title-prefix="{icon: 'fa fa-address-card-o'}"></vxe-form-item>
          <vxe-form-item title="Name" field="name" span="12" :item-render="{name: 'input', attrs: {placeholder: '请输入名称'}}"></vxe-form-item>
          <vxe-form-item title="Nickname" field="nickname" span="12" :item-render="{name: 'input', attrs: {placeholder: '请输入昵称'}}"></vxe-form-item>
          <vxe-form-item title="Role" field="role" span="12" :item-render="{name: 'input', attrs: {placeholder: '请输入角色'}}"></vxe-form-item>
          <vxe-form-item title="Sex" field="sex" span="12" :item-render="{name: '$select', options: sexList}"></vxe-form-item>
          <vxe-form-item title="Age" field="age" span="12" :item-render="{name: 'input', attrs: {type: 'number', placeholder: '请输入年龄'}}"></vxe-form-item>
          <vxe-form-item title="Other information" span="24" title-align="left" title-width="200px" :title-prefix="{message: '请填写必填项', icon: 'fa fa-info-circle'}"></vxe-form-item>
          <vxe-form-item title="Number" field="num" span="12" :item-render="{name: 'input', attrs: {type: 'number', placeholder: '请输入数值'}}"></vxe-form-item>
          <vxe-form-item title="Date" field="date3" span="12" :item-render="{name: '$input', props: {type: 'date', placeholder: '请选择日期'}}"></vxe-form-item>
          <vxe-form-item title="Address" field="address" span="24" :title-suffix="{message: '啦啦啦，就是这么强大！！！', icon: 'fa fa-question-circle'}" :item-render="{name: 'textarea', attrs: {placeholder: '请输入地址'}}"></vxe-form-item>
          <vxe-form-item align="center" span="24">
            <template #default>
              <vxe-button type="submit" status="primary">保存</vxe-button>
              <vxe-button type="reset">重置</vxe-button>
              <vxe-button @click="$refs.xModal.close()">取消</vxe-button>
            </template>
          </vxe-form-item>
        </vxe-form>
      </template>
    </vxe-modal>

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
      selectRow: null,
      showEdit: false,
      sexList: [
        { label: '', value: '' },
        { label: '女', value: '0' },
        { label: '男', value: '1' }
      ],
      formData: null,
      formRules: {
        name: [
          { required: true, message: '请输入名称' },
          { min: 3, max: 5, message: '长度在 3 到 5 个字符' }
        ],
        nickname: [
          { required: true, message: '请输入昵称' }
        ],
        sex: [
          { required: true, message: '请选择性别' }
        ]
      },
      tableData: [
        { id: 10001, name: 'Test1', role: 'Develop', sex: '0', age: 28, amount: 888, address: 'test abc' },
        { id: 10002, name: 'Test2', role: 'Test', sex: '1', age: 22, amount: 666, address: 'Guangzhou' },
        { id: 10003, name: 'Test3', role: 'PM', sex: '1', age: 32, amount: 89, address: 'Shanghai' },
        { id: 10004, name: 'Test4', role: 'Designer', sex: '0', age: 23, amount: 1000, address: 'test abc' },
        { id: 10005, name: 'Test5', role: 'Develop', sex: '0', age: 30, amount: 999, address: 'Shanghai' },
        { id: 10006, name: 'Test6', role: 'Designer', sex: '0', age: 21, amount: 998, address: 'test abc' },
        { id: 10007, name: 'Test7', role: 'Test', sex: '1', age: 29, amount: 2000, address: 'test abc' },
        { id: 10008, name: 'Test8', role: 'Develop', sex: '1', age: 35, amount: 999, address: 'test abc' },
        { id: 10009, name: 'Test9', role: 'Test', sex: '1', age: 26, amount: 2000, address: 'test abc' },
        { id: 100010, name: 'Test10', role: 'Develop', sex: '1', age: 21, amount: 666, address: 'test abc' }
      ],
      demoCodes: [
        `
        <vxe-table
          border
          resizable
          highlight-hover-row
          highlight-current-row
          height="500"
          :data="tableData">
          <vxe-column type="seq" width="60"></vxe-column>
          <vxe-column field="name" title="Name"></vxe-column>
          <vxe-column field="sex" title="Sex" :formatter="formatterSex"></vxe-column>
          <vxe-column field="age" title="Age"></vxe-column>
          <vxe-column field="address" title="Address" show-overflow></vxe-column>
          <vxe-column title="操作" width="100" show-overflow>
            <template #default="{ row }">
              <vxe-button type="text" icon="fa fa-edit" @click="editEvent(row)"></vxe-button>
              <vxe-button type="text" icon="fa fa-trash-o"></vxe-button>
            </template>
          </vxe-column>
        </vxe-table>

        <vxe-modal ref="xModal" v-model="showEdit" title="编辑&保存" width="800" resize destroy-on-close>
          <template #default>
            <vxe-form :data="formData" :rules="formRules" title-align="right" title-width="100" @submit="submitEvent">
              <vxe-form-item title="Basic information" span="24" title-align="left" title-width="200px" :title-prefix="{icon: 'fa fa-address-card-o'}"></vxe-form-item>
              <vxe-form-item title="Name" field="name" span="12" :item-render="{name: 'input', attrs: {placeholder: '请输入名称'}}"></vxe-form-item>
              <vxe-form-item title="Nickname" field="nickname" span="12" :item-render="{name: 'input', attrs: {placeholder: '请输入昵称'}}"></vxe-form-item>
              <vxe-form-item title="Role" field="role" span="12" :item-render="{name: 'input', attrs: {placeholder: '请输入角色'}}"></vxe-form-item>
              <vxe-form-item title="Sex" field="sex" span="12" :item-render="{name: '$select', options: sexList}"></vxe-form-item>
              <vxe-form-item title="Age" field="age" span="12" :item-render="{name: 'input', attrs: {type: 'number', placeholder: '请输入年龄'}}"></vxe-form-item>
              <vxe-form-item title="Other information" span="24" title-align="left" title-width="200px" :title-prefix="{message: '请填写必填项', icon: 'fa fa-info-circle'}"></vxe-form-item>
              <vxe-form-item title="Number" field="num" span="12" :item-render="{name: 'input', attrs: {type: 'number', placeholder: '请输入数值'}}"></vxe-form-item>
              <vxe-form-item title="Date" field="date3" span="12" :item-render="{name: '$input', props: {type: 'date', placeholder: '请选择日期'}}"></vxe-form-item>
              <vxe-form-item title="Address" field="address" span="24" :title-suffix="{message: '啦啦啦，就是这么强大！！！', icon: 'fa fa-question-circle'}" :item-render="{name: 'textarea', attrs: {placeholder: '请输入地址'}}"></vxe-form-item>
              <vxe-form-item align="center" span="24">
                <template #default>
                  <vxe-button type="submit" status="primary">保存</vxe-button>
                  <vxe-button type="reset">重置</vxe-button>
                  <vxe-button @click="$refs.xModal.close()">取消</vxe-button>
                </template>
              </vxe-form-item>
            </vxe-form>
          </template>
        </vxe-modal>
        `,
        `
        export default {
          data () {
            return {
              selectRow: null,
              showEdit: false,
              sexList: [
                { label: '', value: '' },
                { label: '女', value: '0' },
                { label: '男', value: '1' }
              ],
              formData: null,
              formRules: {
                name: [
                  { required: true, message: '请输入名称' },
                  { min: 3, max: 5, message: '长度在 3 到 5 个字符' }
                ],
                nickname: [
                  { required: true, message: '请输入昵称' }
                ],
                sex: [
                  { required: true, message: '请选择性别' }
                ]
              },
              tableData: [
                { id: 10001, name: 'Test1', role: 'Develop', sex: '0', age: 28, amount: 888, address: 'test abc' },
                { id: 10002, name: 'Test2', role: 'Test', sex: '1', age: 22, amount: 666, address: 'Guangzhou' },
                { id: 10003, name: 'Test3', role: 'PM', sex: '1', age: 32, amount: 89, address: 'Shanghai' },
                { id: 10004, name: 'Test4', role: 'Designer', sex: '0', age: 23, amount: 1000, address: 'test abc' },
                { id: 10005, name: 'Test5', role: 'Develop', sex: '0', age: 30, amount: 999, address: 'Shanghai' },
                { id: 10006, name: 'Test6', role: 'Designer', sex: '0', age: 21, amount: 998, address: 'test abc' },
                { id: 10007, name: 'Test7', role: 'Test', sex: '1', age: 29, amount: 2000, address: 'test abc' },
                { id: 10008, name: 'Test8', role: 'Develop', sex: '1', age: 35, amount: 999, address: 'test abc' },
                { id: 10009, name: 'Test9', role: 'Test', sex: '1', age: 26, amount: 2000, address: 'test abc' },
                { id: 100010, name: 'Test10', role: 'Develop', sex: '1', age: 21, amount: 666, address: 'test abc' }
              ]
            }
          },
          methods: {
            formatterSex ({ cellValue }) {
              const item = this.sexList.find(item => item.value === cellValue)
              return item ? item.label : ''
            },
            editEvent (row) {
              this.formData = {
                name: row.name,
                nickname: row.nickname,
                role: row.role,
                sex: row.sex,
                age: row.age,
                num: row.num,
                date3: row.date3,
                address: row.address
              }
              this.selectRow = row
              this.showEdit = true
            },
            submitEvent () {
              this.showEdit = false
              this.$XModal.message({ content: '保存成功', status: 'success' })
              Object.assign(this.selectRow, this.formData)
            }
          }
        }
        `
      ]
    }
  },
  methods: {
    formatterSex ({ cellValue }) {
      const item = this.sexList.find(item => item.value === cellValue)
      return item ? item.label : ''
    },
    editEvent (row) {
      this.formData = {
        name: row.name,
        nickname: row.nickname,
        role: row.role,
        sex: row.sex,
        age: row.age,
        num: row.num,
        date3: row.date3,
        address: row.address
      }
      this.selectRow = row
      this.showEdit = true
    },
    submitEvent () {
      this.showEdit = false
      this.$XModal.message({ content: '保存成功', status: 'success' })
      Object.assign(this.selectRow, this.formData)
    }
  }
}
</script>
