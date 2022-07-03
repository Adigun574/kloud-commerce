<template>
  <div>
    <Loader v-if="users.length === 0" />

    <div class="bg-white p-4" v-if="users.length > 0">
      <div
        class="
          flex
          justify-between
          items-center
          border-b-1 border-solid border-inherit
          pb-2
          mb-4
        "
      >
        <p class="grey-text"><b>View All Users</b></p>
        <button
          data-toggle="modal" data-target="#exampleModal"
          class="
            bg-blue-500
            hover:bg-blue-700
            text-white
            font-bold
            py-2
            px-4
            rounded
          "
          @click="setUserAction('Create')"
        >
          Create New User
        </button>
      </div>

      <div
        class="
          bg-[#f1f2f5]
          mb-2
          flex
          justify-between
          items-center
          py-2
          pl-6
          pr-2
          overflow-x-auto
          sm:flex
          hidden
        "
      >
        <p class="bg-white p-2 rounded text-xs cursor-pointer"><i class="fa fa-search"></i></p>
        <div class="grey-text">
          <div class="mt-4 flex justify-end items-center">
            <div class="mr-3">
              <p><b>1</b> - <b>{{user.length}}</b> of <b>{{users.length}}</b> Entriesss</p>
            </div>
            <b-pagination
              v-model="currentPage"
              :total-rows="rows"
              :per-page="perPage"
              first-number
              last-number
            ></b-pagination>
            <div class="bg-white flex items-center ml-3 px-2 mb-3 rounded">
              <p class="relative rows-p"><b>Rows:</b></p>
              <select>
                <option>10</option>
              </select>
            </div>
          </div>
        </div>
      </div>

      <div
        class="
          bg-[#f1f2f5]
          mb-2
          p-4
          sm:hidden
        "
      >
        <div class="flex justify-between items-center"> 
            <div class="mr-3">
              <p><b>1</b> - <b>{{user.length}}</b> of <b>{{users.length}}</b> Entries</p>
            </div>
            <b-pagination
              v-model="currentPage"
              :total-rows="rows"
              :per-page="perPage"
              first-number
              last-number
            ></b-pagination>
        </div>

        <div class="flex justify-between"> 
            <input class="form-control" type="search"/>
            <div class="bg-white flex items-center ml-3 px-2 mb-3 rounded">
              <p class="relative rows-p"><b>Rows:</b></p>
              <select>
                <option>10</option>
              </select>
            </div>
        </div>

      </div>

      <!---->

      <div class="overflow-x-auto grey-text">
        <table
          class="w-full border-1 border-solid border-[#e1e5ee] overflow-x-auto"
        >
          <thead class="bg-[#f8f9fa]">
            <tr class="border-b-1 border-solid border-[#e1e5ee]">
              <th>S/N</th>
              <th>NAME</th>
              <th>EMAIL</th>
              <th>PHONE NUMBER</th>
              <th>ACTIONS</th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="(user, index) in users"
              :key="user.id"
              class="border-b-1 border-solid border-[#e1e5ee]"
            >
              <td>{{ index + 1 }}</td>
              <td> <span class="initials text-white mr-2">{{user.name.split(' ')[0].split('')[0]}}{{user.name.split(' ')[1].split('')[0]}}</span> {{ user.name }}</td>
              <td>{{ user.email }}</td>
              <td>{{ user.phone }}</td>
              <td>
                <div class="flex">
                  <button @click="setUserAction('Edit'); openEditModal(user)" data-toggle="modal" data-target="#exampleModal" class="mr-4 bg-[#f5faff] p-1 px-2 rounded">
                    <i class="fa fa-edit text-blue-400"></i>
                  </button>
                  <button
                    @click="deleteUser(user)"
                    class="mr-4 bg-[#fef5f5] p-1 px-2 rounded"
                  >
                    <i class="fa fa-trash text-rose-500"></i>
                  </button>
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>

      <div class="mt-4 flex justify-end">
        <div class="grey-text">
          <div class="mt-4 flex justify-end items-center">
            <div class="mr-3">
              <p><b>1</b> - <b>{{user.length}}</b> of <b>{{users.length}}</b> Entries</p>
            </div>
            <b-pagination
              v-model="currentPage"
              :total-rows="rows"
              :per-page="perPage"
              first-number
              last-number
            ></b-pagination>
            <div class="bg-white flex items-center ml-3 px-2 mb-3 rounded border-1 border-inherit border-solid">
              <p class="relative rows-p"><b>Rows:</b></p>
              <select>
                <option>10</option>
              </select>
            </div>
          </div>
        </div>
      </div>
    </div>



    <!-- Modal -->
        <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div class="modal-dialog" role="document">
                <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="exampleModalLabel">{{userAction}} User</h5>
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                    <span aria-hidden="true">&times;</span>
                    </button>
                </div>
                <div class="modal-body">
                    <!---->
                    <form class="w-full max-w-lg">
                        <div class="flex flex-wrap -mx-3 mb-6">
                            <div class="w-full md:w-1/2 px-3 mb-6 md:mb-0">
                            <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="grid-first-name">
                                First Name
                            </label>
                            <input v-model="user.firstName" class="appearance-none block w-full bg-gray-200 text-gray-700 border border-red-500 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white" id="grid-first-name" type="text" placeholder="John">
                            <p v-if="submitted && !user.firstName" class="text-red-500 text-xs italic">Please fill out this field.</p>
                            </div>
                            <div class="w-full md:w-1/2 px-3">
                            <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="grid-last-name">
                                Last Name
                            </label>
                            <input v-model="user.lastName" class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" id="grid-last-name" type="text" placeholder="Doe">
                            <p v-if="submitted && !user.lastName" class="text-red-500 text-xs italic">Please fill out this field.</p>
                            </div>
                        </div>
                        <div class="flex flex-wrap -mx-3 mb-6">
                            <div class="w-full px-3">
                            <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="grid-email">
                                Email
                            </label>
                            <input v-model="user.email" class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" id="grid-email" type="grid-email" placeholder="johndoe@example.com">
                            <p v-if="submitted && !user.email" class="text-red-500 text-xs italic">Invalid Email</p>
                            </div>
                        </div>
                        <div class="flex flex-wrap -mx-3 mb-6">
                            <div class="w-full px-3">
                            <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="grid-phone">
                                Phone Number
                            </label>
                            <input v-model="user.phone" class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" id="grid-phone" type="text" placeholder="2348012345678">
                            <p v-if="submitted && !user.phone" class="text-red-500 text-xs italic">Invalid Phone Number</p>
                            </div>
                        </div>
                    </form>

                    <!---->
                </div>
                
                <div class="flex justify-end pb-4 pr-4">
                    <template v-if="!loading">
                        <button type="button" class="bg-rose-500 hover:bg-rose-700 text-white font-bold py-2 px-4 rounded mr-2" data-dismiss="modal">Close</button>
                        <button v-if="userAction === 'Create'" @click="saveUser()" type="button" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">Save</button>
                        <button v-if="userAction === 'Edit'" @click="editUser()" type="button" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">Update</button>
                    </template>
                    <template v-if="loading">
                        <div class="spinner-border" role="status">
                            <span class="sr-only">Loading...</span>
                        </div>
                    </template>
                </div>
                </div>
            </div>
        </div>
      <!---->
  </div>
</template>

<script>
import axios from 'axios';
import Swal from 'sweetalert2'
import Loader from './Loader.vue';


export default {

  data() {
    return {
        page: 1,
        url:'https://jsonplaceholder.typicode.com/users',
        users: [],
        perPage: 10,
        currentPage: 1,
        user:{
            firstName:'',
            lastName:'',
            email:'',
            phone:''
        },
        submitted: false,
        loading: false,
        userAction: '',
        userId: null
      }
  },
  computed: {
      rows() {
        return this.users.length
      }
  },
  created() {
    this.getUsers()
  },
  mounted(){
  },
  methods: {
    getUsers(){
      axios.get(this.url)
      .then(response => {
        this.users = response.data
      })
      .catch(error => {
        this.makeToast('danger', 'Error', 'Something went wrong')
      })
    },
    deleteUser(user){
      console.log(user)
      Swal.fire({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        icon: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, delete it!'
      }).then((result) => {
        if (result.isConfirmed) {
          //call delete method
          axios.delete(`${this.url}/${1}`)
            .then(response => {
                this.makeToast('success', 'Success', 'User has been deleted')
            })
            .catch(error => {
                this.makeToast('danger', 'Error', 'Something went wrong')
            })
        }
      })
    },
    saveUser(){
        this.submitted = false
        if(this.user.firstName && this.user.lastName && this.user.email && this.user.phone){
            console.log(this.user)
            this.loading = true
            axios.post(this.url, this.user)
            .then(response => {
                console.log(response)
                this.loading = false
                $('#exampleModal').modal('hide')
                this.makeToast('success', 'Success', 'User has been saved')
                this.resetUserForm()
            })
            .catch(error => {
                console.log(error);
                this.loading = false
                $('#exampleModal').modal('hide')
                this.makeToast('danger', 'Error', 'Something went wrong')
                this.resetUserForm()
            })
        }
        else{
            this.submitted = true
        }
    },
    makeToast(variant, title, content) {
        this.$bvToast.toast(`${content}`, {
          title: `${title}`,
          variant: variant,
          solid: true,
        //   autoHideDelay: 3000
        })
    },
    resetUserForm(){
        this.user = {
            firstName:'',
            lastName:'',
            email:'',
            phone:''
        }
    },
    setUserAction(action){
        this.user = {
            firstName:'',
            lastName:'',
            email:'',
            phone:''
        }
        this.userAction = action
    },
    openEditModal(user){
        this.user = {
            firstName: user.name.split(' ')[0],
            lastName: user.name.split(' ')[1],
            email: user.email,
            phone: user.phone
        }
        this.userId = user.id
    },
    editUser(user){
        if(this.user.firstName && this.user.lastName && this.user.email && this.user.phone){
            this.loading = true
            axios.put(`${this.url}/${this.userId}`, this.user)
            .then(response => {
                console.log(response)
                this.loading = false
                $('#exampleModal').modal('hide')
                this.makeToast('success', 'Success', 'User has been updated')
                this.resetUserForm()
            })
            .catch(error => {
                console.log(error);
                this.loading = false
                $('#exampleModal').modal('hide')
                this.makeToast('danger', 'Error', 'Something went wrong')
                this.resetUserForm()
            })
        }
        else{

        }
    }

  },
  components: {
    Loader
  }
}
</script>


<style scoped>
  .app-body{
    background-color: #f4f5fa;
  }
  th, td {
    padding: 15px;
  }
  .initials{
      background-color: #4780f8;
      border-radius: 50%;
      padding:10px;
      font-size: 12px;
  }
  .grey-text{
    color: #616469
  }
  .rows-p{
      top:7px;
  }
  
</style>