<template>
  <div>
    <table class="table">
      <thead>
        <th>Tarefa</th>
        <th></th>
      </thead>
      <tbody v-for="(todo, index) in todos" :key="index">
        <td class="description">{{ todo.description }}</td>
        <td>
          <ButtonVue
            icon="pi pi-pencil"
            class="p-button-rounded p-button-text"
            @click="$emit('edit', index)"
          ></ButtonVue>
        </td>
        <td>
          <ButtonVue
            icon="pi pi-trash"
            class="p-button-rounded p-button-text"
            @click="$emit('deleta', index)"
          ></ButtonVue>
        </td>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    todos: Array,
  },
};
</script>

<style scoped>
.table {
  margin-top: 2rem;
}
.description {
  flex-grow: 1;
}
</style>