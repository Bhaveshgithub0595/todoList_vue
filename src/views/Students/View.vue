<template>
  <div class="container">
    <div class="card">
      <div class="card-header">
        <h4>
          Students
          <RouterLink to="/students/create" class="btn btn-primary   "
            >Add Student</RouterLink
          >
        </h4>
      </div>
      <div class="card-body">
        <table class="table table-bordered">
          <thead>
            <tr>
              <th>ID</th>
              <th>Name</th>
              <th>Age</th>
              <th>Gender</th>
              <th>Email</th>
              <th>Phone</th>
              <th>Courses</th>
              <th>gpa</th>
              <th>image</th>
            </tr>
          </thead>
          <tbody v-if="this.students.length > 0" >
            <tr v-for="(student, index) in this.students" :key="index">
              <td>{{ student.id }}</td>
              <td>{{ student.name }}</td>
              <td>{{ student.age }}</td>
              <td>{{ student.gender }}</td> 
              <td>{{ student.email }}</td>
              <td>{{ student.phone }}</td>
              <td>{{ student.courses }}</td>
              <td>{{ student.gpa }}</td>
              <td>{{ student.image }}</td>
              <td>
                <RouterLink :to="{path: '/students/'+student.id+'/edit'}" class="btn btn-success">Edit</RouterLink>
                <button type="button" @click="deleteStudent(student.id)" class="btn btn-danger">Delete</button>
              </td>
            </tr>
          </tbody>
          <tbody v-else  >
            <tr>
                <td colspan="10">Loading....</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "students",
  data() {
    return {
      students: [],
    };
  },
  mounted() {
    // console.log("I am here");
    // Now we have to call the data here
    this.getStudents();
  },
  methods: {
    getStudents() {
      axios.get("https://freetestapi.com/api/v1/students").then((res) => {
        this.students = res.data;
        // console.log(this.students);
      });
    },

    deleteStudent(studentId){
 

        if(confirm('Are you sure you want to delete this data?')){

            // console.log(studentId);
            axios.delete("https://freetestapi.com/api/v1/students").then(res =>{

            })
        }
    }
  },
};
</script>
