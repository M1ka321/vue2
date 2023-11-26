<template>
  <el-dialog title="Форма создания" :visible.sync="localVisible" @close="handleCancel">
    <el-form :model="localFormData" ref="createForm" label-position="left" label-width="80px">
      <el-form-item label="Название" prop="name">
        <el-input v-model="localFormData.name" autocomplete="off"></el-input>
      </el-form-item>
      <el-form-item label="Статус" prop="status">
        <el-select v-model="localFormData.status" placeholder="Выберете статус">
          <el-option label="Создан" value="1"></el-option>
          <el-option label="Проведен" value="2"></el-option>
          <el-option label="Отменен" value="3"></el-option>
        </el-select>
      </el-form-item>
    </el-form>
    <span slot="footer" class="dialog-footer">
      <el-button @click="handleCancel">Отмена</el-button>
      <el-button type="primary" @click="handleConfirm">Создать</el-button>
    </span>
  </el-dialog>
</template>

<script>
export default {
  props: {
    visible: Boolean
  },
  data() {
    return {
      localVisible: this.visible,
      localFormData: {
        name: "",
        status: ""
      }
    };
  },
  watch: {
    visible(newVal) {
      this.localVisible = newVal;
      this.localFormData = {
        name: "",
        status: ""
      };
    }
  },
  methods: {
    handleCancel() {
      this.$emit("update:visible", false);
    },
    handleConfirm() {
      this.$emit("update:visible", false);
      this.$emit("save", {...this.localFormData});
    }
  }
};
</script>