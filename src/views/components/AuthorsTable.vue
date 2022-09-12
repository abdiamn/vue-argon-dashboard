<template>
  <div class="card">
    <div class="card-header pb-0">
      <h6>Users table</h6>
    </div>
    <div class="card-body px-0 pt-0 pb-2">
      <div class="table-responsive p-0">
        <table class="table align-items-center mb-0">
          <thead>
            <tr>
              <th class="text-uppercase text-secondary text-xxs font-weight-bolder opacity-7">Name</th>
              <th class="text-uppercase text-secondary text-xxs font-weight-bolder opacity-7 ps-2">Email</th>
              <th class="text-center text-uppercase text-secondary text-xxs font-weight-bolder opacity-7">Status</th>
              <th class="text-secondary opacity-7"></th>
            </tr>
          </thead>
          <tbody v-if="get && get.length">
            <tr v-for="get of get">
              <td>
                <div class="d-flex px-2 py-1">
                  <div>
                    <img :src=get.avatar class="avatar avatar-sm me-3" alt="user1" />
                  </div>
                  <div class="d-flex flex-column justify-content-center">
                    <h6 class="mb-0 text-sm">{{get.first_name}}</h6>
                    <p class="text-xs text-secondary mb-0">{{get.last_name}}</p>
                  </div>
                </div>
              </td>
              <td>
                <p class="text-xs font-weight-bold mb-0">{{get.email}}</p>
              </td>
              <td class="align-middle text-center text-sm">
                <span class="badge badge-sm bg-gradient-success">Online</span>
              </td>
              <td class="align-middle">
                <a href="javascript:;" class="text-danger font-weight-bold text-xs" data-toggle="tooltip"
                  data-original-title="Delete user">Delete</a>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios';
export default {
  name: "authors-table",
  data() {
    return {
      get: []
    }
  },
  created() {
    axios.get('https://reqres.in/api/users')
      .then(response => {
        this.get = response.data.data
      })
  },
  async deleteUser() {
    let x = window.confirm("You want to delete the user?");

    if (x) {
      const user = await axios.delete("https://reqres.in/api/users/2");

      console.log(user);
      alert("User deleted!");
    }
  },
};
</script>
