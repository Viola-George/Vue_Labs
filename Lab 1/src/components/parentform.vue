<template>
  <!-- <adminChild />
  <userChild /> -->
  <div>
    <div class="d-flex gap-5 justify-content-center align-items-center">
      <button type="button" class="btn btn-info" @click="toggleForm">
        Form view
      </button>
      <button type="button" class="btn btn-dark" @click="toggleAdmin">
        Admins Table
      </button>
      <button type="button" class="btn btn-dark" @click="toggleUser">
        User Table
      </button>
    </div>
    <adminChild v-if="showAdmin" @deletingAdmin="deleteAdmin" @deletingUser="deleteUser" />
    <userChild v-if="showUser" @deletingStudent="deleteStudent" @deletingUser="deleteUser"/>
    <div id="formContainer" v-if="showForm" class="w-50 m-auto bg-info mt-5">
      <div class="fw-bold text-center my-2"><p>Registration</p></div>
      <form @submit.prevent="addUser">
        <div class="row mb-3">
          <div class="col-3">
            <label for="exampleInputEmail1" class="form-label pt-2">Name</label>
          </div>
          <div class="col-9">
            <input
            type="text"
            class="form-control"
            id="exampleInputEmail1"
            aria-describedby="emailHelp"
            v-model="user.name"
          />
          </div>
         
        </div>
        <div class="row mb-3">
          <div class="col-3">
            <label for="exampleInputEmail1" class="form-label label pt-2">Age</label>
          </div>  
          <div class="col-9">
            <input
            type="text"
            class="form-control"
            id="exampleInputPassword1"
            v-model="user.age"
          />
          </div>
        </div>
        <div class="form-check form-check-inline">
          <input
            class="form-check-input"
            type="radio"
            name="inlineRadioOptions"
            id="adminRole"
            value="admin"
            v-model="user.role"
          />
          <label class="form-check-label" for="inlineRadio1">Admin</label>
        </div>
        <div class="form-check form-check-inline">
          <input
            class="form-check-input"
            type="radio"
            name="inlineRadioOptions"
            id="userRole"
            value="user"
            v-model="user.role"
          />
          <label class="form-check-label" for="inlineRadio2">User</label>
        </div>

        <button type="submit" id="mybtn" class="btn bg-black">Submit</button>
      </form>
    </div>
  </div>
</template>

<script>
import adminChild from "./adminchild.vue";
import userChild from "./userchild.vue";
export default {
  name: "formParent",
  components: {
    adminChild,
    userChild,
  },
  provide() {
    return {
      allUsers: this.allUsers,
    };
  },
  data() {
    return {
      user: {},
      allUsers: [],
      showForm: true,

      showAdmin: false,
      showUser: false,
    };
  },

  methods: {
    addUser() {
      this.allUsers.push(this.user);
      this.user = [];
      console.log(this.allUsers);
    },
    toggleForm() {
      this.showAdmin = false;
      this.showUser = false;
      this.showForm = true;
    },
    toggleAdmin() {
      this.showUser = false;
      this.showForm = false;
      this.showAdmin = true;
    },
    toggleUser() {
      this.showAdmin = false;
      this.showForm = false;
      this.showUser = true;
    },
    deleteUser(index){
        this.allUsers.splice(index, 1);
    }
  },
};
</script>

<style scoped>
#formContainer {
  padding: 20px;
  margin: auto;
  border-radius: 5%;
  width: 50%;
  height: 30%;
}
#mybtn{
  color: white;
  margin-left: 40%;
}
.label{
  font-size: larger;
}
</style>
