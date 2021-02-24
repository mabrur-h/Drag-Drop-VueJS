<template>
  <v-container>
      <v-row
        class="card-wrapper"
      >
        <div
            v-for="column in columns"
            :key="column.title"
            class="card"
        >
          <div class="tasks-title-wrapper">
            <h2
                v-text="column.title"
                :class="column.class"
                class="tasks-title"></h2>
<!--            <p class="tasks-subtitle">Add an issue</p>-->
          </div>
          <draggable :list="column.tasks" :animation="200" ghost-class="ghost-card" group="tasks" style="min-height: 200px">
            <v-card
                class="mx-auto card-element"
                max-width="344"
                v-for="task in column.tasks"
                :key="task.id"
            >
              <v-card-text>
                <h3
                    class="tasks-element-title"
                    v-text="task.title"
                >
                </h3>
                <p
                    class="tasks-date"
                    v-text="task.date"
                ></p>
              </v-card-text>
            </v-card>
          </draggable>
        </div>
        <div class="task-add">
          <button class="add-button" @click="showModal = true">+</button>
        </div>
        <transition name="fade" appear>
          <div class="modal-overlay" v-if="showModal" @click="showModal = false"></div>
        </transition>
        <transition name="slide" appear>
          <div class="modal" v-if="showModal">
            <h1>Add new task</h1>
            <div>
              <input type="text" class="text-input" placeholder="task..." v-model="newTask">
              <input type="text" class="text-input" placeholder="deadline..." v-model="newDeadline">
            </div>
            <button class="button btn-add">
              Add task
            </button>
            <button class="button btn-cancel" @click="showModal = false">
              Cancel
            </button>
          </div>
        </transition>

      </v-row>

  </v-container>
</template>

<script>
import draggable from 'vuedraggable';

export default {
  components: {
    draggable
  },

  data() {
    return {
      columns: [
        {
          title: 'Ideas/Tasks',
          class: 'tasks-bg',
          tasks: [
            {
              id: 1,
              title: 'New Sidebar design',
              date: '20:00 / 22:00'
            },
            {
              id: 2,
              title: 'Header design features',
              date: '00:00 / 20:00'
            }
          ]
        },
        {
          title: 'In Progress',
          class: 'in-progress-bg',
          tasks: [
            {
              id: 3,
              title: 'Login Error',
              date: '04:10 / 22:00'
            }
          ]
        },
        {
          title: 'Needs review',
          class: 'reviews-bg',
          tasks: [
            {
              id: 4,
              title: 'Onboarding Screens',
              date: '22:30 / 23:30'
            },
            {
              id: 5,
              title: 'Dashboard design',
              date: '22:30 / 23:30'
            }
          ]
        },
        {
          title: 'Approved',
          class: 'approved-bg',
          tasks: [
            {
              id: 6,
              title: 'Account settings screen',
              date: '22:30 / 23:30'
            },
            {
              id: 7,
              title: 'Mobile layout',
              date: '22:30 / 23:30'
            }
          ]
        }
      ],
      showModal: false,
      issue: '',
      newDeadline: '',
      newTask: '',
    }
  },
  methods: {
    addElement() {

    }
  }
}
</script>

<style>
@import 'assets/css/style.css';
</style>