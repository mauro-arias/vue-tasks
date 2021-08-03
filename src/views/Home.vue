<template>
  <div>
    <v-container class='mt-5' grid-list-xl>
      <v-layout row>
        
        <!-- Formulario de agregar -->

        <v-flex xs12 sm6 v-if='formAdd'>
          <h1 class='display-1 text-center'>Agregar tarea</h1>
          <v-card class='my-3 pa-3' >
            <v-form @submit.prevent='addTask'>
              <v-textarea @keyup.enter='addTask' v-model='description' auto-grow rows='1' label='¿Qué tienes que realizar?'></v-textarea >
              <v-btn type="submit" block color='cyan' dark small>Agregar tarea<v-icon right>mdi-send</v-icon></v-btn>
            </v-form>
            <div class='mt-3 d-flex align-center'>
              <v-icon small>mdi-information</v-icon><p class='mb-0 ml-2 text-caption'>Ningún dato es guardado, siéntete libre de probar la aplicación.</p>
            </div>
          </v-card>
        </v-flex>

        <!-- Formulario de editar -->

        <v-flex xs12 sm6 v-if="!formAdd">
          <h1 class='display-1 text-center'>Editar tarea</h1>
          <v-card class='my-3 pa-3' >
            <v-form @submit.prevent='editTask'>
              <v-textarea @keyup.enter='editTask' v-model='description' auto-grow rows='1' label='¿Qué tienes que realizar?'></v-textarea >
              <v-btn type="submit" block color='success' dark small>Editar tarea<v-icon right>mdi-send</v-icon></v-btn>
            </v-form>
          </v-card>
        </v-flex>

        <!-- Listado de tareas -->


        <v-flex xs12 sm6>
          <h1 class='display-1 text-center'>Lista de tareas</h1>

          <v-card-text v-if='taskList.length === 0' class='d-flex justify-center mt-3'><p class='mb-0 font-weight-medium'>No hay ninguna tarea aún...</p></v-card-text>

          <v-card class='my-3' elevation="4" v-for='(task, index) in taskList' :key='index'>
            <v-card-title><v-chip color='cyan' label text-color="white"><v-icon left>mdi-label</v-icon>Tarea N° {{ task.id }}</v-chip></v-card-title>
            <v-card-text><p class='mb-0'>{{ task.description }}</p></v-card-text>
            <v-card-actions>
              <v-btn small text color='info' @click='edit(index)'>Editar</v-btn>
              <v-btn small text color='error' @click='deleteTask(task.id)'>Eliminar</v-btn>
            </v-card-actions>
          </v-card>
        </v-flex>

      </v-layout>



      <v-snackbar v-model="snackbar" timeout='1500' color='cyan' left top>
        {{ text }}

        <template v-slot:action="{ attrs }">
          <v-btn color="white" text v-bind="attrs" @click="snackbar = false"><v-icon>mdi-close</v-icon></v-btn>
        </template>
      </v-snackbar>


    </v-container>
  </div>
</template>

<script>

  export default {
    name: 'Home',

    components: {
    },
    data(){
      return {
        taskList : [],
        description: '',
        snackbar: false,
        text: '',
        formAdd: true,
        indexTask: ''
      }
    },
    methods: {
      addTask(){
        if (this.description.trim() === ''){
          this.text = 'La tarea está vacía!'
          this.snackbar = true;
          this.description = '';
        } else {
          this.taskList.push({
            id: this.taskList.length + 1,
            description : this.description
          })
          
          this.snackbar = true;
          this.text = 'Tarea agregada!'

        }

        this.description = '';
      },
      deleteTask(id){
        this.taskList = this.taskList.filter(e => e.id != id);

        this.snackbar = true;
        this.text = 'Tarea eliminada!'
      },
      edit(index){
        this.formAdd = false;
        this.description = this.taskList[index].description;
        this.indexTask = index;
      },
      editTask(){
        this.taskList[this.indexTask].description = this.description;
        this.formAdd = true;
        this.description = '';

        this.snackbar = true;
        this.text = 'Tarea actualizada!'
      }
    }
  }
</script>
