<script setup>
import { computed, onMounted, ref, watch } from "vue";

const todos = ref([]);
const name = ref("");

const input_content = ref(""); //입력내용
const input_category = ref(null);

//입력값을 todos배열에 넣는 함수
const addTodo = () => {
  if (input_content.value.trim() === "" || input_category.value === null) {
    return;
  }
  todos.value.push({
    content: input_content.value,
    category: input_category.value,
    createAt: new Date().getTime(),
    done: false,
    editable: false,
  });
  //입력 후 초기화
  input_content.value = "";
  input_category.value = null;
  console.log("todos: ", todos);
};

//시간순으로 순서 정리( b.createAt - a.createAt :새로운 todo가 위에 보임)
const todos_asc = computed(() =>
  todos.value.sort((a, b) => {
    return b.createAt - a.createAt;
  })
);

//삭제 함수
const remoeveTodo = (todo) => {
  todos.value = todos.value.filter((t) => t !== todo);
};

//이름입력하는 것을 인지하고 로컬스토리지에 저장,업데이트
watch(name, (newVal) => {
  localStorage.setItem("name", newVal);
});

//todos가 변하는 것을 인지하고 로컬스토리지 저장,업데이트
watch(
  todos,
  (newVal) => {
    localStorage.setItem("todos", JSON.stringify(newVal));
  },
  { deep: true }
); //deep -프로퍼티나, 하위 뎁스값도 감시

//새로열었을때 로컬스토리지에서 불러오기(없을때는 비워놈)
onMounted(() => {
  name.value = localStorage.getItem("name") || "";
  todos.value = JSON.parse(localStorage.getItem("todos") || []);
});
</script>

<template>
  <main class="app">
    <section class="greeting">
      <h1 class="title">
        "오늘"은 흘러가는 것이 아니라 채워가는 것
        <input type="text" placeholder="name here" v-model="name" />
      </h1>
    </section>

    <section class="create-todo">
      <h2>오늘 하루 계획을 세워 완성해보세요.</h2>
      <form id="new-todo-form" v-on:submit.prevent="addTodo">
        <h4>오늘 할 일 목록</h4>
        <input
          type="text"
          id="content"
          placeholder="ex)typescript 토이 프로젝트 만들기"
          v-model="input_content"
        />
        <!-- {{ input_content  }} -->
        <div class="options">
          <label>
            <input
              type="radio"
              name="category"
              id="categogy1"
              value="business"
              v-model="input_category"
            />
            <span class="bubble business"></span>
            <div>공부</div>
          </label>
          <label>
            <input
              type="radio"
              name="category"
              id="categogy2"
              value="personal"
              v-model="input_category"
            />
            <span class="bubble personal"></span>
            <div>여가 생활</div>
          </label>
        </div>
        <!-- {{ input_category }} -->
        <input type="submit" value="Click!" class="plus-btn" />
      </form>
    </section>

    <section class="todo-list">
      <h3>TODO LIST</h3>
      <div class="list" id="todo-list">
        <div
          v-for="(todo, index) in todos_asc"
          :key="index"
          v-bind:class="`todo-item ${todo.done && 'done'}`"
        >
          <label>
            <input type="checkbox" v-model="todo.done" />
            <span :class="`bubble ${todo.category}`"></span>
          </label>

          <div class="todo-content">
            <input type="text" v-model="todo.content" />
          </div>
          <div class="actions">
            <button class="delete" @click="remoeveTodo(todo)">Delete</button>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>
