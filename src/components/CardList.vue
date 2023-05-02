<template>
    <div>
      <h1>Список задач:</h1>
      <ul>
        <li v-for="card in cards" :key="card.id" class="card">
          <h2>{{ card.title }}</h2>
          <p>{{ card.completed ? 'Выполнено' : 'Не выполнено' }}</p>
          <button @click="handleDelete(card.id)">Удалить</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        cards: [],
      };
    },
    methods: {
      deleteCard(cardId) {
        const cardIndex = this.cards.findIndex(card => card.id === cardId);
        if (cardIndex !== -1) {
          this.cards.splice(cardIndex, 1);
        }
      },
      handleDelete(cardId) {
        this.deleteCard(cardId);
        this.cards = this.cards.filter(card => card.id !== cardId);
      },
    },
    mounted() {
      axios.get('https://jsonplaceholder.typicode.com/todos')
        .then(response => {
          this.cards = response.data;
        })
        .catch(error => {
          console.log(error);
        });
    },
  };
  </script>
  
  <style>
  .card {
    background-color: #fff;
    border: 1px solid #cccccc;
    padding: 10px;
    margin-bottom: 10px;
  }
  </style>