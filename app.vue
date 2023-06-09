<template>
  <div>
    <div class="list-task">
      <h2> To Do list </h2>
      <p v-if="tasks.length == 0"> Belum ada Task </p>
      <div v-for="item,index of tasks" class="item-task d-flex align-items-start border-bottom pt-3 pb-4">
        <input
        type="checkbox"
        name="status"
        id="task"
        class="me-2 mt-2"
        :checked="item.isDone"
        @click="complete(index)"
        >
        <div class="d-flex flex-column">
          <div v-if="tasks[index].status" class="title-task mb-1" style="text-decoration: line-through;">
            {{ item.title }}
          </div>
          <div v-else class="title-task mb-1">
            {{ item.title }}
          </div>
          <div class="description-task small text-muted">
            {{ item.description }}
          </div>
          <div>
            <a href="#" @click="tasks.splice(index, 1);">Delete</a>
          </div>
          <div>
          </div>
        </div>
      </div>

    </div>
    <div class="action py-2">
      <a href="#" class="add-button" v-if="!isCreating" @click="isCreating =
!isCreating">Add Task</a>
    <div class="add-card" v-else>
      <div class="card mb-2">
        <div class="card-body d-flex flex-column p-0">
          <form ref="inputForm" @submit="submitForm">
          <input v-model="titleValue" class="form-control border-0 mb-2" placeholder="Title" type="text">
          <textarea v-model="descriptionValue" class="form-control border-0 small" placeholder="Description" rows="3"></textarea>
          </form>
        </div>
    </div>
    <div class="button-wrapper d-flex">
      <button class="btn btn-primary me-2" @click="addTask">Save</button>
      <button class="btn btn-outline-secondary" @click="isCreating =
!isCreating">Cancel</button>
    </div>
  </div>
  </div>
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

export default {
  data() {
    return {
      tasks: [
      ],
          isCreating: false,
          titleValue: '',
          descriptionValue: '',
    }
  },
  methods: {
    addTask() {
      console.log('title: ', this.titleValue);
      console.log('description: ', this.descriptionValue);
      this.tasks.push({
        title: this.titleValue,
        description: this.descriptionValue,
        isDone: false,
      });
      this.titleValue = ''
      this.descriptionValue = ''
    },
    complete(index) {
      this.tasks[index].status = !this.tasks[index].status
    }
}
}

</script>
