<template>
  <div class="container mx-auto sm:px-4">
    <div class="table-wrapper">
      <div class="table-title">
        <div class="flex flex-wrap">
          <div class="sm:w-1/2 pr-4 pl-4">
            <h2>User <b>Management</b></h2>
          </div>
          <div class=" flex justify-end sm:w-1/2 pr-4 pl-4">
            <router-link to="/about"
              class="flex gap-3 inline-block align-middle text-center select-none border font-normal whitespace-no-wrap rounded py-1 px-3 leading-normal no-underline bg-green-500 text-white hover:green-600"
              data-toggle="modal"><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                <path stroke-linecap="round" stroke-linejoin="round"
                  d="M12 9v6m3-3H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
              <span>Add New Employee</span>
            </router-link>
          </div>
        </div>
      </div>
      <table class="w-full max-w-full mb-4 bg-transparent table-striped ">
        <thead>
          <tr>
            <th></th>
            <th>Name</th>
            <th>Email</th>
            <th>Username</th>
            <th>Phone</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <GetUser :root="root" />
        </tbody>
      </table>
    </div>
  </div>
</template>
<script>
import GetUser from "./GetUser.vue";
export default {
  name: "UserTable",
  async mounted() {
    const userTable = JSON.parse(localStorage.getItem("userTable"));
    if (userTable && userTable.length) {
      this.root.push(...userTable);
    }
    else {
      await fetch("https://dummyjson.com/users")
        .then((res) => res.json())
        .then((res) => {
          if (res) {
            this.root.push(...res.users)
            localStorage.setItem("userTable", JSON.stringify(this.root));
          }
        })
    }
  },
  data() {
    return {
      root: []
    };
  },
  components: { GetUser }
}
</script>
<style  scoped>
.table-wrapper {
  min-width: 1000px;
  background: #fff;
  padding: 20px 25px;
  border-radius: 3px;
  box-shadow: 0 1px 1px rgba(0, 0, 0, .05);
}

.table-title {
  padding-bottom: 15px;
  background: #435d7d;
  color: #fff;
  padding: 16px 30px;
  margin: -20px -25px 10px;
  border-radius: 3px 3px 0 0;
}
</style>
