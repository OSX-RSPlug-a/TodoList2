<template>
    <div class="q-pa-md" style="z-index: 1">
    <q-layout view="lHh lpr lFf" container style="margin-top: 10%; height: 300px; z-index: 1" class="shadow-2 rounded-borders">
      <q-header elevated>
        <q-toolbar>
          <div class="row q-pa-lg-sm bg-primary">

            <q-input
              v-model="newTask"
              @keyup.enter="addTask" 
              class="col" 
              square
              placeholder="Add task" 
              dense>
              <template v-slot:append>
                <q-btn 
                @click="addTask"
                round 
                dense 
                flat 
                icon="add" />
              </template>
              </q-input>
            </div>

          </q-toolbar>
      </q-header>

      <q-page-container style="z-index: 1">
          <q-list
          separator
          bordered
          >
            <q-item 
              v-for="(task, index) in tasks"
              :key="task.title"
              @click="task.done = !task.done"
              :class="{ 'done bg-blue-1': task.done }"
              clickable
              v-riple>
              <q-item-section avatar>
                <q-checkbox 
                  v-model="task.done" 
                  class="no-pointer-events"
                  color="secondary" />
              </q-item-section>
              <q-item-section>
                <q-item-label>{{ task.title }}</q-item-label>
              </q-item-section>
              <q-item-section
              v-if="task.done"
              side>
                <q-btn 
                @click.stop="deleteTask(index)"
                flat 
                round 
                dense 
                color="secundary" 
                icon="delete" 
                style="z-index: 0"/>
              </q-item-section>
            </q-item>
          </q-list>
      </q-page-container>
    </q-layout>
    <div
    v-if="!tasks.length" 
    class="no-tasks absolute-center">
        <q-icon name="check" size="100px" color="secundary" />
        <div class="text-h5 text-secondary text-center">
          No Tasks
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PageIndex',
  data() {
    return{
      newTask: '',
      tasks: [
        //{
        //  title: 'Test',
        //  done: false
        //},
        //{
        //  title: 'Test1',
        //  done: false
        //},
        //{
        //  title: 'Test2',
        //  done: false
       // }
      ]
    }
  },
  methods: {
    deleteTask(index) {
      this.$q.dialog({
        title: 'Confirm',
        message: 'Delete?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks.splice(index, 1)
        this.$q.notify('Task deleted')
      })
    },
    addTask() {
      this.tasks.push({
        title: this.newTask,
        done: false
      })
      this.newTask = ''
    }
  }
}
</script>

<style lang="scss">
.done {
  .q-item__label {
    text-decoration: line-through;
    color: #bbbbbb
  }
}
.no-tasks {
  margin-top: 5%;
  opacity: 0.6;
}
  @media screen and(max-width: 455px){
    .q-layout {
      margin-top: 15%;
    }
  }
</style>