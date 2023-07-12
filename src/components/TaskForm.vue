<template>
  <div class="task-form">
    <h3>Добавить задачу</h3>
    <form @submit.prevent="addTask">
      <div class="form-group">
        <label for="title"></label>
        <input
          id="title"
          v-model="title"
          required
          placeholder="Укажите заголовок задачи"
        />
      </div>
      <div class="form-group">
        <label for="description"></label>
        <textarea
          id="description"
          v-model="description"
          required
          placeholder="Укажите описание задачи"
        ></textarea>
      </div>
      <button type="submit">Добавить</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      description: "",
    };
  },
  methods: {
    addTask() {
      const newTask = {
        id: Date.now(),
        title: this.title,
        description: this.description,
        completed: false,
      };
      this.$emit("addTask", newTask);
      this.title = "";
      this.description = "";
    },
  },
};
</script>

<style lang="scss">
.task-form {
  text-align: left;
  padding: 30px;
  background-color: #ffffff;
  border: 1px solid #cccccc;
  border-radius: 4px;
  display: flex;
  align-items: flex-start;
  flex-direction: column;

  h3 {
    font-size: 18px;
    margin-bottom: 10px;
  }

  form {
    display: flex;
    flex-direction: column;
    align-items: flex-start;

    .form-group {
      margin-bottom: 10px;

      label {
        display: block;
        margin-bottom: 5px;
        font-weight: bold;
      }

      input,
      textarea {
        padding: 5px;
        font-size: 14px;
        border: 1px solid #cccccc;
        border-radius: 4px;
        width: 530px;
        box-sizing: border-box;

        &:focus {
          outline: none;
          border-color: #007bff;
          box-shadow: 0 0 0 2px rgba(0, 123, 255, 0.25);
        }
      }
    }

    button {
      padding: 5px 10px;
      margin: 0 auto;
      font-size: 14px;
      background-color: #007bff;
      color: #ffffff;
      border: none;
      border-radius: 4px;
      cursor: pointer;

      &:hover {
        background-color: #0056b3;
      }
    }
  }
}
</style>
