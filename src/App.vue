<template>
  <div id="app">
    <TableComponent/>
    <EditFormComponent/>
    <CreateFormComponent/>
  </div>
</template>

<script>
import TableComponent from "@/components/TableComponent.vue";
import EditFormComponent from "@/components/EditFormComponent.vue";
import CreateFormComponent from "@/components/CreateFormComponent.vue";

export default {
  name: 'App',
  components: {
    TableComponent,
    EditFormComponent,
    CreateFormComponent
  },
}
</script>
