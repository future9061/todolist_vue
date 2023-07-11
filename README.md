# todolist_vue


<br>


### vue로 만드는 Todolist
<br>


## 🖥️ 프로젝트 소개
vue.js
<br>

## 🕰️ 개발 기간
* 23.07.11일 ~ 미정
<br>


## ⚙️ 개발 환경
- `vs code 1.77`
- **Framework** : 
- **Database** : 
- **library** : 
<br>


## 📌 주요 기능
#### 
- 

<br>


## 🎇code review

- **사용자 이름을 input에 입력하면 localStorage에 저장 및 localStorage에서 빼오기**

```ruby

<script setup>
import { ref } from 'vue';
  
  const name = ref("");
  
  watch(name,(newVal)=>{  
    localStorage.setItem("name", newVal);
  })

  onMounted(() => {
  name.value = localStorage.getItem("name") || "";
});
  
</script>



  <template>
    <div>
      <h1 class="title">
        What's name
        <input type="text" placeholder="name here" v-model="name" />
        {{ name }}
      </h1>
    </div>
  </template>
  
```


**사용한 문법**


  1. __v-model : 양방향 바인딩 구현__
        
        
        <input type="text" placeholder="name here" v-model="name"/>
        {{ name }}
        
   
   
  __ref : 전달된 데이터를 저장, 단일 속성 .value로 데이터 변경하여 반응형 객체를 반환한다
  value로 새 값을 할당, 읽기 작업, 쓰기 작업 가능__


      <script setup>
            const count = ref(0)
            console.log(count.value) //0
      
            const increment = () =>{
             count.value++
            }
      </script>
      
      <template>
           <p>{{ count.value }}</p>
           <button v-on:click="increment">숫자 증가</button>
      </template>
      


   __watch : 데이터 변경 시 호출될 감시 콜백을 선언 (특정 변수 변화 감지)__

    watch(name, (newVal) => {
    localStorage.setItem("name", newVal);
    });
    watch(변수, ()=>{콜백함수})



   __onMounted : 컴포넌트가 마운트된 후 호출될 콜백을 등록, 서버 사이트 렌더링 중에 호출되지 않음.
   App component가 마운트 된 후 실행__
   
    onMounted(() => {
    name.value = localStorage.getItem("name") || "";
    });

   

     
   

- **작성한 todolist 입력값과 options 값 저장하기**


```ruby
<script setup>

  const todos = ref([]); //입력값을 todos 배열에 push로 저장
  const input_content = ref(""); //입력내용
  const input_category = ref(null);//옵션


//입력값을 todos 배열에 넣는 함수
// const addTodo = () => {
//   if (input_content.value.trim() === "") return;
//   todos.value.push({
//     content: input_content.value,
//   });
// };

</script>


<template>

//할 일 입력 input
 <input
  type="text"
  id="content"
  placeholder="할일을 입력해주세요"
  v-model="input_content"/>
  {{ input_content }}


//옵션 입력 input
<label>
  <input
    type="radio"
    name="category"
    id="category1"
    value="business"
    v-model="input_category"
   />
  <div>business</div>
</label>

<label>
  <input
    type="radio"
    name="category"
    id="category2"
    value="personal"
    v-model="input_category"
   />
  <div>personal</div>
</label>
  {{ input_category }}

</template>
```


## 🔧upgrade 예정

- 
