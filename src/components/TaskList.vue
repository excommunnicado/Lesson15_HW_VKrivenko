<template>
  <div class="task-list">
    <h2>Список задач</h2>
    <div class="task-summary">
      <p>Общее количество задач: {{ totalTasks }}</p>
      <p>Количество выполненных задач: {{ completedTasks }}</p>
    </div>

    <!-- Добавить задачу -->
    <div class="add-task-section">
      <TaskForm @addTask="addTask" />
    </div>

    <!-- Список задач -->
    <ul class="task-items">
      <li
        v-for="task in tasks"
        :key="task.id"
        :class="[
          'task-item',
          { completed: task.completed, 'not-completed': !task.completed },
        ]"
      >
        <TaskItem
          :task="task"
          @deleteTask="deleteTask"
          @toggleComplete="toggleComplete"
        >
          <template v-slot:details>
            <p>Полное описание задачи: {{ task.description }}</p>
          </template>
        </TaskItem>
      </li>
    </ul>
  </div>
</template>

<script>
import TaskItem from "./TaskItem.vue";
import TaskForm from "./TaskForm.vue";

export default {
  components: {
    TaskItem,
    TaskForm,
  },
  data() {
    return {
      tasks: [
        {
          id: 1,
          title: "Купить хлеб",
          description: "Свежий, французский багет",
          completed: false,
        },
        {
          id: 2,
          title: "Перелет",
          description: "Алматы-Шымкент, в рейс в 19:30",
          completed: false,
        },
        {
          id: 3,
          title: "Посетить концерт",
          description: "Poets of the fall, 15.07, в 20:00",
          completed: false,
        },
      ],
    };
  },
  computed: {
    totalTasks() {
      return this.tasks.length;
    },
    completedTasks() {
      return this.tasks.filter((task) => task.completed).length;
    },
  },
  methods: {
    addTask(newTask) {
      this.tasks.push(newTask);
    },
    deleteTask(taskId) {
      this.tasks = this.tasks.filter((task) => task.id !== taskId);
    },
    toggleComplete(taskId) {
      const task = this.tasks.find((task) => task.id === taskId);
      if (task) {
        task.completed = !task.completed;
      }
    },
  },
};
</script>

<style>
.task-list {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f4f4f4;
  border-radius: 4px;
  text-align: left;
}

.add-task-section {
  margin: 20px 0px;
}

.task-items {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.task-items li {
  padding: 10px;
  background-color: #ffffff;
  border: 1px solid #cccccc;
  border-radius: 4px;
  display: flex;
  align-items: center;
}

.task-list .task-items li button {
  padding: 5px 10px;
  font-size: 14px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.task-list .task-items li button.toggle-button {
  background-color: #007bff;
  color: #ffffff;
}

.task-list .task-items li button.toggle-button:hover {
  background-color: #0056b3;
}

.task-list .task-items li button.delete-button {
  background-color: #dc3545;
  color: #ffffff;
}

.task-list .task-items li button.delete-button:hover {
  background-color: #a71d2a;
}

.task-list .task-items li button.details-button {
  background-color: #28a745;
  color: #ffffff;
}

.task-list .task-items li button.details-button:hover {
  background-color: #1f8d3e;
}

li.completed {
  display: flex;
  justify-content: center;
  text-decoration: line-through;
  color: #808080;
  background-color: #8ff9a8;
}

li.not-completed {
  background-color: #f8d7da;
  display: flex;
  justify-content: center;
  align-items: center;
}

.task-list .task-items li .status {
  font-weight: bold;
}

.task-list .task-items li .status.completed {
  color: #28a745;
}

.task-list .task-items li .status.not-completed {
  color: #dc3545;
}
</style>
