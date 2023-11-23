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

    <EditFormComponent :visible.sync="dialogFormVisible" :formData="editForm" @save="saveEditForm" />
    <CreateFormComponent :visible.sync="createFormVisible" @save="saveCreateForm" />
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
      this.editForm = { ...row };
    },
    openCreateForm() {
      this.createFormVisible = true;
    },
    saveEditForm() {
      //изменение дописать
      this.dialogFormVisible = false;
    },
    saveCreateForm() {
      //добавление дописать
      this.createFormVisible = false;
    },
    deleteSelected() {
      // удаление дописать
      this.selectedRows = [];
    }
  },
  components: {
    EditFormComponent,
    CreateFormComponent
  }
};
</script>
