<template>
  <div id="app">
<!--Insert components in the order wanted to be seen in the app-->
<!--parent receives message with v-on then call the function it will use-->
    <new-student-form v-on:student-added="newStudentAdded"></new-student-form>
<!--use v-bind to receive prop data from child components-->
    <StudentTable v-bind:students="students"
                  v-on:student-arrived-or-left="studentArrivedOrLeft"
                  v-on:delete-student="deleteStudent"></StudentTable>
    <StudentMessage v-bind:student="mostRecentStudent"></StudentMessage>
  </div>
</template>

<script>
import NewStudentForm from './components/NewStudentForm.vue'
import StudentMessage from './components/StudentMessage.vue'
import StudentTable from './components/StudentTable.vue'

export default {
  name: 'App',
  components: {
    NewStudentForm,
    StudentMessage,
    StudentTable
  },
  data(){
    return{
      students:[],
      mostRecentStudent:{

      }
    }
  },
  methods: {
    newStudentAdded(student){
      this.students.push(student)
      this.students.sort(function (s1,s2){
        return s1.name.toLowerCase() < s2.name.toLowerCase() ? -1 : 1
      })
    },
    studentArrivedOrLeft(student, present){
      //need to find the student then update present attribute
      let updateStudent = this.students.find(function (s){
        if (s.name === student.name && s.starID === student.starID){
          //return true if they match
          return true
        }
      })

      if (updateStudent){
        updateStudent.present = present
        this.mostRecentStudent = updateStudent
      }
    },
    deleteStudent(student){
      this.students = this.students.filter(function (s){
        if (s !== student){
          return true
        }
      })
    }
  }
}
</script>

<style>
@import "https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css";
</style>
