<template>
  <div class="Home__page" :style="{ backgroundColor: backgroundColor }">
    <div class="Home__title">
      <h1 :style="{ color: titleColor }">TODO LIST</h1>
      <TaskLIst @onBlack="blackBag" />
      <CreateTask
        v-if="ShowCreateTask"
        @ClickClose="HandleButtonClick"
        @dataSent="addTask"
      />
      <div
        class="Home__item"
        v-for="(task, index) in tasks"
        :key="task.id"
        :style="{ color: titleColor }"
      >
        <div class="Home__text">
          <input
            class="Home__input"
            type="checkbox"
            name=""
            id=""
            @click="deleteTask(index)"
          />
          {{ task.text }}
        </div>
        <div class="Home__function">
          <img class="Home__edit" src="../assets/img/Frame 6.svg" alt="" />
          <img
            class="Home__delete"
            src="../assets/img/frame5.svg"
            alt=""
            @click="deleteTask(index)"
          />
        </div>
      </div>
      <img
        class="Home__add"
        src="../assets/img/Add button.svg"
        alt=""
        @click="CreateTask"
      />
    </div>
  </div>
</template>

<script>
import TaskLIst from "@/components/TaskLIst.vue";
import CreateTask from "@/components/common/CreateTask.vue";

export default {
  name: "HomePage",
  components: {
    TaskLIst,
    CreateTask,
  },
  data() {
    return {
      isWhite: true,
      ShowCreateTask: false,
      tasks: [],
      backgroundColor: "white",
    };
  },
  created() {
    this.loadTasks();
  },
  computed: {
    backgroundColor() {
      return this.isWhite ? "white" : "black";
    },
    titleColor() {
      return this.isWhite ? "black" : "white";
    },
  },
  methods: {
    blackBag() {
      this.isWhite = !this.isWhite;
    },
    CreateTask() {
      this.ShowCreateTask = !this.ShowCreateTask;
    },
    HandleButtonClick() {
      this.ShowCreateTask = false; // Закрываем форму
    },
    addTask(data) {
      const newTask = { id: Date.now(), text: data };
      this.tasks.push(newTask);
      this.saveTasks(); // Сохраняем в localStorage
      this.ShowCreateTask = false; // Закрываем форму
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
      this.saveTasks(); // Сохраняем изменения
    },
    loadTasks() {
      const savedTasks = localStorage.getItem("tasks");
      this.tasks = savedTasks ? JSON.parse(savedTasks) : [];
    },
    saveTasks() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
    updateTask(updatedTask) {
      const taskIndex = this.tasks.findIndex(
        (task) => task.id === updatedTask.id
      );
      if (taskIndex !== -1) {
        this.tasks[taskIndex].text = updatedTask.text;
        this.saveTasks(); // Сохраняем изменения в localStorage
      }
    },
  },
};
</script>
<style lang="scss" scoped>
@import "@/assets/style/main.scss";

.Home__page {
  padding: 0px 20px;
  background-color: $white;
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: background-color 0.5s;
}

.Home__title {
  width: 100%;
  display: flex;
  flex-direction: column;
  max-width: 850px;
  max-height: 750px;
  height: 100%;
  position: relative;

  & h1 {
    margin-top: 40px;
    margin-bottom: 18px;
    font-family: $font-family;
    font-weight: 500;
    font-size: 26px;
    color: $black;
    text-align: center;
  }

  .Home__edit {
    margin-right: 10px;
    &:hover {
      opacity: 0.5;
      transition: all 0.2s ease-in;
    }
  }
  .Home__delete {
    &:hover {
      opacity: 0.5;
      transition: all 0.2s ease-in;
    }
  }
}
.Home__add {
  position: absolute;
  bottom: 32px;
  right: 50px;
}
.Home__item {
  border-bottom: 1px solid rgba($purple, 0.5);
  margin-top: 30px;
  margin-left: 70px;
  max-width: 520px;
  width: 100%;
  align-items: center;
  text-align: center;
  display: flex;
  justify-content: space-between;
}
.Home__text {
  margin-bottom: 10px;
  font-family: $font-family;
  font-weight: 500;
  font-size: 20px;
  line-height: 100%;
  text-transform: uppercase;
  color: $black;
  align-items: center;
  display: flex;
}

[type="checkbox"] {
  width: 26px;
  height: 26px;
  margin-right: 17px;
  border: 1px solid $purple;
  border-radius: 2px;
}

.Home__function {
  display: flex;
  justify-content: right;
  max-width: 100px;
  width: 100px;
}
</style>
