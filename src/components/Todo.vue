<template>
  <main>
    <section class="glass">
      <h1>TODO</h1>
      <div class="list" id="items">
        <ul id="task" v-for="todo in todoList">
          <li>
            <span class="todo-id">{{ todo.id }}</span>
            <span class="todo-text">{{ todo.text }}</span>
            <img
              src="https://upload.wikimedia.org/wikipedia/commons/a/a3/Delete-button.svg"
              width="20px"
              @click="deleteTodo(todo.id)"
            />
          </li>
        </ul>
      </div>
      <div class="footer">
        <input
          v-model="currentTodo"
          type="text"
          id="ip"
          placeholder="Add your goals for today."
        />
        <button @click="addTodo" id="btn">ADD</button>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },

  data() {
    return {
      currentTodo: "",
      todoList: JSON.parse(localStorage.getItem("todoList")),
    };
  },

  methods: {
    addTodo() {
      if (this.currentTodo === "") {
        alert("Todo can't be Empty");
      } else {
        const newTodo = {
          id: this.todoList.length + 1,
          text: this.currentTodo,
        };
        this.todoList.push(newTodo);
        this.currentTodo = "";
        localStorage.setItem("todoList", JSON.stringify(this.todoList));
      }
    },

    deleteTodo(id) {
      console.log(localStorage.getItem("todoList"));
      this.todoList = this.todoList.filter((item) => item.id !== id);
      this.todoList = this.todoList.map((item, index) => {
        return { ...item, id: index + 1 };
      });

      localStorage.setItem("todoList", JSON.stringify(this.todoList));
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >
@import url("https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,400;0,500;0,600;0,700;0,800;0,900;1,500&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: poppins;
}

main {
  min-height: 100vh;
  background: linear-gradient(to right top, #65dfc9, #6cdbeb);
  display: flex;
  align-items: center;
  justify-content: center;
}

.glass {
  background-color: white;
  min-height: 80vh;

  width: min(25rem, 90%);
  background: linear-gradient(
    to right bottom,
    rgba(255, 255, 255, 0.7),
    rgba(255, 255, 255, 0.3)
  );
  border-radius: 0.5rem;
  position: relative;
}

h1 {
  text-align: center;
  margin: 1.5rem;
  font-weight: bold;
}

.list {
  height: 60vh;
  padding-bottom: 2em;
  overflow-y: auto;
  overflow-x: hidden;
}

li {
  list-style-type: none;
  margin-left: 1.2rem;
  margin-right: 1.2rem;
  margin-bottom: 0.19rem;
  padding: 3px 20px;
  border-radius: 40px;
  background-color: white;

  animation: addTodo 0.2s ease-out;

  display: flex;
  justify-content: space-between;
  align-items: center;
}

li > span.todo-id {
  font-weight: 800;
}

li > span.todo-text {
  width: 90%;
  padding: 0em 1em;
  overflow-wrap: break-word;
}

#btn {
  width: 15%;
  font-weight: 900;
  margin-right: 1.2rem;
  background-color: #d6190f;
  color: white;
  border: none;
  border-radius: 100px;
}

#btn:hover {
  background-color: #751611;
}

.footer {
  display: flex;
  position: absolute;
  bottom: 1.8rem;
  height: 1.7rem;
  width: 100%;
}

.footer input {
  width: 85%;
  margin-left: 1.2rem;
  margin-right: 10px;
  padding: 3px;
  padding-left: 15px;
  font-size: 17px;
  border: none;
  border-radius: 20px;
}

@keyframes addTodo {
  0% {
    transform: translateX(-100%);
  }

  60% {
    transform: translateX(10%);
  }

  80% {
    transform: translateX(-10%);
  }

  100% {
    transform: translateX(0%);
  }
}
</style>
