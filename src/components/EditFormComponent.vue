<template>
  <el-dialog title="Форма редактирования" :visible.sync="localVisible">
    <el-form :model="localFormData" ref="editForm" label-position="left" label-width="80px">
      <el-form-item label="Название" prop="name">
        <el-input v-model="localFormData.name" autocomplete="off"></el-input>
      </el-form-item>
      <el-form-item label="Статус" prop="status">
        <el-select v-model="localFormData.status" placeholder="Выберете статус">
          <el-option v-for="option in statusOptions" :key="option.value" :label="option.label" :value="option.value"></el-option>
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
    formData: Object,
    statusOptions: Array
  },
  data() {
    return {
      localVisible: this.visible,
      localFormData: { ...this.formData },
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
        this.$emit("save", { ...this.localFormData, status: parseInt(this.localFormData.status, 10) });

        },
  }
};
</script>
