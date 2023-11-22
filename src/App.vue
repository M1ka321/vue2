<template>
  <div id="app">
    <Navbar/>
    <el-table
        :data="tableData"
        style="width: 100%">
      <el-table-column
          prop="id"
          label="Идентификатор"
          width="180">
      </el-table-column>
      <el-table-column
          prop="name"
          label="Название"
          width="180">
      </el-table-column>
      <el-table-column
          prop="status_id"
          label="Статус">
      </el-table-column>
      <el-table-column
          prop="created_at"
          label="Дата создания">
      </el-table-column>
      <el-table-column>
        <el-button>Удалить</el-button>
      </el-table-column>
    </el-table>
    <TableForm/>
  </div>
</template>
<script>
import TableForm from "@/components/TableForm.vue";
import Navbar from "@/components/Navbar.vue";

export default {
  name: 'App',
  components: {
    TableForm,
    Navbar
  },
  data() {
    return {
      tableData: [
        {
          id: 1,
          name: "Приходная накладная",
          status_id: 1,
          created_at: "2023-07-04 11:00:00.207814"
        },
        {
          "id": 2,
          "name": "Расходная накладная",
          "status_id": 2,
          "created_at": "2023-07-04 11:00:00.207814"
        }
      ]
    }
  }


}
</script>

