<template>
  <div>
    <el-button type="primary" @click="openCreateForm">Создать</el-button>
    <el-button type="danger" @click="deleteSelected">Удалить</el-button>

    <el-table :data="tableData" @row-click="openEditForm" :default-sort="{ prop: 'id', order: 'ascending' }">
      <el-table-column type="selection" width="55"></el-table-column>
      <el-table-column prop="id" label="Идентификатор" min-width="18px"></el-table-column>
      <el-table-column prop="name" label="Название"></el-table-column>
      <el-table-column prop="status" label="Статус"></el-table-column>
      <el-table-column prop="created_at" label="Дата создания" width="180"></el-table-column>
    </el-table>

    <EditFormComponent :visible.sync="dialogFormVisible" :formData="editForm" @save="saveEditForm"/>
    <CreateFormComponent :visible.sync="createFormVisible" @save="saveCreateForm"/>
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
          id: 1,
          name: "Приходная накладная",
          status: "Создан",
          created_at: "2023-07-04 11:00:00.207814"
        },
        {
          id: 2,
          name: "Расходная накладная",
          status: "Проведен",
          created_at: "2023-07-04 11:00:00.207814"
        }
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
    openEditForm(row) {
      this.dialogFormVisible = true;
      this.editForm = {...row};
    },
    openCreateForm() {
      this.createFormVisible = true;
      this.editForm = {
        id: null,
        name: "",
        status: ""
      };
    },
    saveEditForm() {
      const index = this.tableData.findIndex(item => item.id === this.editForm.id);

      if (index !== -1) {
        this.tableData[index] = {...this.editForm};
        this.dialogFormVisible = false;
      }
      console.log('Данные после сохранения формы редактирования:', this.tableData);
    },
    saveCreateForm() {
      const newId = this.tableData.length + 1;

      const newRecord = {
        id: newId,
        name: this.editForm.name,
        status: this.editForm.status,
        created_at: new Date().toISOString()
      };
      this.tableData.push(newRecord);
      this.createFormVisible = false;
      console.log('Данные после сохранения формы создания:', this.tableData);
    },

    deleteSelected() {
      this.tableData = this.tableData.filter(item => !this.selectedRows.includes(item));
      this.selectedRows = [];
      console.log('Данные после удаления выбранных строк:', this.tableData);
    }
  },
  components: {
    EditFormComponent,
    CreateFormComponent
  }
};
</script>
