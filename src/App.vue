Votre code présen
<template>
  <form action="" @submit.prevent="addTodo">
    <fieldset role="group">
      <input v-model="newTodo" placeholder="Tâche à faire">
      <button type="submit">Ajouter</button>
    </fieldset>
  </form>
  
  <div v-if="todos.length === 0">Aucune tâche à faire.</div>
  
  <ul>
    <li v-for="todo in filteredTodos" :key="todo.date" :class="{ completed: todo.completed }">
      <input type="checkbox" v-model="todo.completed">
      {{ todo.title }}
    </li>
  </ul>
  
  <div>
    <label>
      <input type="checkbox" v-model="hideCompleted">
      Masquer les tâches terminées
    </label>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// Variables réactives
const newTodo = ref('')

const todos = ref([])

const hideCompleted = ref(false)

// Fonction pour ajouter une nouvelle tâche
const addTodo = () => {
  if (newTodo.value.trim()) {
    todos.value.push({
      title: newTodo.value,
      completed: false,
      date: Date.now()
    })
    newTodo.value = ''
  }
}

// Computed property pour filtrer les tâches
const filteredTodos = computed(() => {
  return hideCompleted.value
    ? todos.value.filter(todo => !todo.completed)
    : todos.value
})
</script>

<style>
.completed {
  text-decoration: line-through;
}
</style>
```

### Explications et améliorations :
1. **Ajout de la tâche** : La fonction `addTodo` vérifie d'abord que le champ `newTodo` n'est pas vide avant d'ajouter la tâche. Ensuite, elle ajoute un nouvel objet dans le tableau `todos`, qui contient le titre, l'état `completed` (non fait par défaut), et la date actuelle en tant qu'identifiant unique.

2. **Filtrage des tâches** : Utilisation d'une propriété calculée (`computed`) pour filtrer les tâches en fonction de l'état `hideCompleted`. Si l'utilisateur coche la case "Masquer les tâches terminées", seules les tâches non terminées seront affichées.

3. **CSS** : Ajout d'une classe `.completed` pour barrer les tâches terminées. Vous pouvez personnaliser le style comme vous le souhaitez.

4. **Validation du champ de texte** : La fonction `addTodo` vérifie si `newTodo` contient du texte avant d'ajouter une tâche. Cela empêche d'ajouter des tâches vides.

Ce code devrait maintenant fonctionner correctement et répondre à votre besoin de Todo List avec Vue.js. N'oubliez pas d'installer et de configurer Vue.js correctement dans votre projet pour éviter les erreurs.

