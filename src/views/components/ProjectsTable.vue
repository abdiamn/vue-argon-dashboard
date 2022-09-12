<template>
  <div class="card">
    <div class="card-header pb-0">
      <h6>Create Form</h6>
    </div>
    <div class="card-body px-3 pt-0 pb-2">
      <div class="mb-3">
        <label for="example-text-input" class="form-control-label">Name</label>
        <input type="text" class="form-control" id="Name" v-model="name" />
      </div>
      <div class="mb-3">
        <label for="example-text-input" class="form-control-label">Job</label>
        <input type="text" class="form-control" id="Job" v-model="job" />
      </div>
      <button @click="post()" class="btn btn-primary">Simpan</button>
      <div id="name"></div>
      <div id="job"></div>
    </div>
  </div>
  <br>
  <div class="card">
    <div class="card-header pb-1">
      <h6>Update Form</h6>
    </div>
    <div class="card-body px-3 pt-0 pb-2">
      <div class="mb-3">
        <label for="example-text-input" class="form-control-label">Name</label>
        <input type="text" class="form-control" id="name" v-model="name" />
      </div>
      <div class="mb-3">
        <label for="example-text-input" class="form-control-label">Job</label>
        <input type="text" class="form-control" id="job" v-model="job" />
      </div>
      <button @click="update()" class="btn btn-primary">Submit</button>
      <div id="name"></div>
      <div id="job"></div>
    </div>
  </div>
  <br>
  <div class="card">
    <div class="card-header pb-1">
      <h6>Delete Button</h6>
    </div>
    <div class="card-body px-3 pt-0 pb-2">
      <button @click="deleteUser" class="btn btn-danger mt-3">Delete</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: "projects-table",
  data() {
    return {
      get: []
    }
  },
  methods: {
    async deleteUser() {
      let x = window.confirm("You want to delete the user?");
      if (x) {
        const user = await axios.delete(
          "https://reqres.in/api/users/2"
        );
        console.log(user);
        alert("User deleted!");
      }
    },
    post() {
      axios
        .post("https://reqres.in/api/users", {
          name: this.name,
          job: this.job,
        })
        .then((response) => { })
        .catch((e) => {
          this.errors.push(e);
        });

      document.getElementById("name").innerHTML =
        '<div class="fs-4">Name : ' + this.name + "</div>";
      document.getElementById("job").innerHTML =
        '<div class="fs-4">Job : ' + this.job + "</div>";
    },
    async update() {
      try {
        const user = await axios.put(
          "https://reqres.in/api/users/2",
          {
            name: this.name,
            job: this.job,
          });
        console.log(user);
        alert("User updated!");
      } catch (e) {
        console.log(e);
      }
    },
    async deleteUser() {
      let x = window.confirm("You want to delete the user?");

      if (x) {
        const user = await axios.delete("https://reqres.in/api/users/2");

        console.log(user);
        alert("User deleted!");
      }
    },
  },
}
</script> 