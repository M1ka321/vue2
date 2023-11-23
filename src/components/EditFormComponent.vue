<template>
  <el-dialog title="Форма редактирования" :visible.sync="localVisible">
    <el-form :model="localFormData" ref="editForm" label-position="left" label-width="80px">
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
      <el-button type="primary" @click="handleConfirm">Сохранить</el-button>
    </span>
  </el-dialog>
</template>

<script>
export default {
  props: {
    visible: Boolean,
    formData: Object
  },
  data() {
    return {
      localVisible: this.visible,
      localFormData: { ...this.formData }
    };
  },
  watch: {
    visible(newVal) {
      this.localVisible = newVal;
      this.localFormData = { ...this.formData };
    }
  },
  methods: {
    handleCancel() {
      this.$emit("update:visible", false);
    },
    handleConfirm() {
      this.$emit("update:visible", false);
      this.$emit("save");
    }
  }
};
</script>
