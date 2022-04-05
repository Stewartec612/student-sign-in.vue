<template>
  <div>
    <div class="card student-list m-2 p-2">
      <h4 class="card-title">Student List</h4>

      <div class="edit-table-toggle form-check">
        <input id="edit-table" type="checkbox" class="form-check-input">
        <label for="edit-table" class="form-check-label"> Edit Table..? </label>
      </div>
      <div id="student-table">
        <table class="table">
          <tr>
            <th>Name</th>
            <th>StarID</th>
            <th>Present?</th>
            <th>Delete</th>
          </tr>

          <student-row v-for="student in students"
                       v-bind:student="student"
                      v-bind:key="student.starID"
                      v-bind:edit="editTable"
                      v-on:student-arrived-or-left="arrivedOrLeft"
                      v-on:delete-student="deleteStudent">
          </student-row>

          <!--Each row will have a checkbox, bound to the app's data
          When the checkbox is checked/unchecked, the student will be signed in/out -->

        </table>
      </div>
    </div>

  </div>
</template>

<script>
import StudentRow from "@/components/StudentRow";
export default {
  name: "StudentTable",
  components: {StudentRow},
  emits: ['student-arrived-or-left'],
  //props are used when a parent component needs to get data from a child component
  props:{
    students: Array
  },
  data(){
    return{
      editTable:false
    }
  },
  methods:{
    arrivedOrLeft(student,present){
      //TODO emit message to parent
      this.$emit('student-arrived-or-left', student,present)
    },
    deleteStudent(student){
      this.$emit('delete-student',student)
    }
  }
}
</script>

<style scoped>


</style>