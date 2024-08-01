<template>
  <div class="container mt-5">
    <div class="card">
      <div class="card-header">
        <h4>Edit Students</h4>
      </div>
      <div class="card-body">
        <ul
          class="alert alert-warning"
          v-if="Object.keys(this.errorList).length > 0">
          <li
            class="mb-0 ms-3"
            v-for="(error, index) in this.errorList"
            :key="index">
            {{ error[0] }}
          </li>
        </ul>

        <div class="mb-3">
          <label for="">Name</label>
          <input
            type="text"
            v-model="model.student.name"
            class="form-control" />
        </div>
        <div class="mb-3">
          <label for="">Age</label>
          <input type="text" v-model="model.student.age" class="form-control" />
        </div>
        <div class="mb-3">
          <label for="">Gender</label>
          <input
            type="text"
            v-model="model.student.gender"
            class="form-control" />
        </div>
        <div class="mb-3">
          <label for="">Email</label>
          <input
            type="text"
            v-model="model.student.email"
            class="form-control" />
        </div>
        <div class="mb-3">
          <label for="">Phone</label>
          <input
            type="text"
            v-model="model.student.phone"
            class="form-control" />
        </div>
        <div class="mb-3">
          <label for="">Courses</label>
          <input
            type="text"
            v-model="model.student.name"
            class="form-control" />
        </div>
        <div class="mb-3">
          <label for="">gpa</label>
          <input type="text" v-model="model.student.gpa" class="form-control" />
        </div>
        <div class="mb-3">
          <label for="">image</label>
          <input
            type="text"
            v-model="model.student.image"
            class="form-control" />
        </div>
        <div class="mb-3">
          <button
            type="button"
            @click="savupdateStudent"
            class="btn btn-primary">
            Update
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "studentEdit",
  data() {
    return {
        studentId : '',
      errorList: "",
      model: {
        student: {
          name: "",
          age: "",
          gender: "",
          email: "",
          phone: "",
          course: "",
          gpa: "",
          image: "",
        },
      },
    };
  },
  mounted() {
    // console.log(this.$route.params.id);
    this.studentId = this.$route.params.id;
    this.getStudentData(this.$route.params.id);
    
  },
  methods: {
    getStudentData(studentId) {
      axios
        .get(`https://freetestapi.com/api/v1/students/${studentId}`)
        .then((res) => {
          console.log(res.data);

          this.model.student = res.data;
        })
        .catch(function (error) {
          if (error.response) {
            if (error.response.data == 404) {
              alert(error.response.data);
            }
          }
        });
    },

    updateStudent() {
      var mythis = this;
      axios
        .put(`https://freetestapi.com/api/v1/students/${this.studentId}`, this.model.student)
        .then((res) => {
          console.log(res.data);
          alert(res.data.message);

          this.errorList = "";
        })
        .catch(function (error) {
          if (error.response) {
            if (error.response.data == 422) {
              mythis.errorList = error.response.data.errors;
            }

            if (error.response.data == 404) {
              alert(error.response.data.message)
            }


            // console.log(error.response.data);
            // console.log(error.response.status);
            // console.log(error.response.headers);
          } else if (error.request) {
            console.log(error.request);
          } else {
            // Something happened in setting up the request that triggered an Error
            console.log("Error", error.message);
          }
        });
    },
    
    saveStudent() {
      var mythis = this;
      axios
        .post("https://freetestapi.com/api/v1/students", this.model.student)
        .then((res) => {
          console.log(res.data);
          alert(res.data.message);

          this.model.student = {
            name: "",
            age: "",
            gender: "",
            email: "",
            phone: "",
            course: "",
            gpa: "",
            image: "",
          };
          this.errorList = "";
        })
        .catch(function (error) {
          if (error.response) {
            if (error.response.data == 422) {
              mythis.errorList = error.response.data.errors;
            }
            // console.log(error.response.data);
            // console.log(error.response.status);
            // console.log(error.response.headers);
          } else if (error.request) {
            console.log(error.request);
          } else {
            // Something happened in setting up the request that triggered an Error
            console.log("Error", error.message);
          }
        });
    },
  },
};
</script>
export
