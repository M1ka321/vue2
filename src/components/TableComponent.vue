<template>
  <div>
    <el-button type="primary" @click="openCreateForm">Создать</el-button>
    <el-button type="danger" @click="deleteSelected">Удалить</el-button>

    <el-table :data="tableData" @row-click="openEditForm" @selection-change="handleSelectionChange" :default-sort="{ prop: 'id', order: 'ascending' }">
      <el-table-column type="selection" width="55"></el-table-column>
      <el-table-column prop="id" label="Идентификатор" min-width="18px" ></el-table-column>
      <el-table-column prop="name" label="Название"></el-table-column>
      <el-table-column prop="status" label="Статус" >
        <template v-slot="{ row }">
          {{ getStatusName(row.status) }}
        </template>
      </el-table-column>
      <el-table-column prop="created_at" label="Дата создания" width="180"></el-table-column>
    </el-table>

    <EditFormComponent :visible.sync="dialogFormVisible" :formData="editForm" :statusOptions="statusOptions" @save="saveEditForm"/>
    <CreateFormComponent :visible.sync="createFormVisible" :statusOptions="statusOptions" @save="saveCreateForm"/>
  </div>
</template>

<script>
import EditFormComponent from "@/components/EditFormComponent.vue";
import CreateFormComponent from "@/components/CreateFormComponent.vue";

export default {
  data() {
    return {
      tableData: [
        {
          id: 3,
          name: "Приходная накладная",
          status: 3,
          created_at: "2023-07-02 11:00:00.207814"
        },
        {
          id: 2,
          name: "Приходная накладная",
          status: 2,
          created_at: "2023-07-04 11:00:00.207814"
        },
        {
          id: 1,
          name: "Расходная накладная",
          status: 1,
          created_at: "2023-07-04 11:00:00.207814"
        }
      ],
      statusOptions: [
        { label: 'Создан', value: '1' },
        { label: 'Проведен', value: '2' },
        { label: 'Отменен', value: '3' }
      ],
      dialogFormVisible: false,
      createFormVisible: false,
      editForm: {
        id: null,
        name: "",
        status: ""
      },
      selectedRows: []
    };
  },
  methods: {
    getStatusName(statusId) {
      switch (statusId) {
        case 1:
          return 'Создан';
        case 2:
          return 'Проведен';
        case 3:
          return 'Отменен';
        default:
          return 'Неизвестный статус';
      }
    },
    handleSelectionChange(selection) {
      this.selectedRows = selection;
    },
    openEditForm(row) {
      this.dialogFormVisible = true;
      this.editForm = { ...row, status: row.status.toString() };
    },
    openCreateForm() {
      this.createFormVisible = true;
      this.editForm = {
        id: null,
        name: "",
        status: ""
      };
    },
    saveEditForm(data) {
      const index = this.tableData.findIndex(item => item.id === data.id);

      if (index !== -1) {
        this.$set(this.tableData, index, {...data});
        this.dialogFormVisible = false;
      }
    },
    saveCreateForm(data) {
      const newId = this.tableData.length + 1;

      const newRecord = {
        id: newId,
        name: data.name,
        status: parseInt(data.status, 10),
        created_at: new Date().toISOString()
      };
      this.tableData.push(newRecord);
      this.createFormVisible = false;
    },

    deleteSelected() {
      console.log('Selected Rows:', this.selectedRows);
      this.tableData = this.tableData.filter(item => !this.selectedRows.includes(item));
      this.selectedRows = [];
    }
  },
  components: {
    EditFormComponent,
    CreateFormComponent
  }
};
</script>
