<template>
  <tr v-bind:class="{ present: student.present, absent: !student.present}">
    <td>{{student.name}}</td>
    <td>{{student.starID}}</td>
    <td>
      <input type="checkbox"
             v-bind:checked="student.present"
             v-on:change="arrivedOrLeft(student, $event.target.checked)"></td>
    <td><img  src="@/assets/delete.png" v-on:click="deleteStudent"> </td>
  </tr>
</template>

<script>
export default {
  name: "StudentRow",
  props: {
    student: Object,
    edit: Boolean
  },
  methods:{
    arrivedOrLeft(student, present) {
      this.$emit('arrived-or-left', student, present)
    },
    deleteStudent(){
      this.$emit('delete-student', this.student)
    }
  }
}
</script>

<style scoped>
.present{
  background-color: lightgray;
  color: gray;
  font-style: italic;
}

.absent{
  color: black;
  font-weight: bold;
}


</style>