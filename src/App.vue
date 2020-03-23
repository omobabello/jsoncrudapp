<template>
  <div id="app">
    <div id="cover-spin"></div>
    <div class="card card-default">
      <div class="card-header">Simple CRUD App</div>
      <div class="card-body">
        <button class="btn btn-success" @click="newUserModal()">
          <i class="fa fa-plus"></i>
          Add New User
        </button>
        <br />
        <br />
        <table class="table table-striped table-bordered table-hover" id="table">
          <thead>
            <tr class="thead-dark">
              <th>S/N</th>
              <th>Full Name</th>
              <th>Email</th>
              <th>Phone Number</th>
              <th>City</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(user,ind) in users">
              <td>{{ind + 1}}</td>
              <td>{{user.name}}</td>
              <td>{{user.email}}</td>
              <td>{{user.phone}}</td>
              <td>{{user.address.city}}</td>
              <td>
                <button
                  class="btn btn-sm btn-info"
                  @click="userInfo(user.id)"
                  title="View User Info"
                >
                  <i class="fa fa-info-circle"></i>
                </button>
                <button class="btn btn-sm btn-light" @click="editUserModal(user)" title="Edit User">
                  <i class="fa fa-edit"></i>
                </button>
                <button
                  class="btn btn-sm btn-danger"
                  @click="deleteUser(user.id, user.name)"
                  title="Delete User"
                >
                  <i class="fa fa-trash"></i>
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
    <div class="modal fade" id="userModal" tabindex="-1" role="dialog">
      <div class="modal-dialog modal-dialog-centered" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">User Data</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <div class="alert alert-danger" v-if="msg.length  > 0" v-html="msg"></div>
            <div class="form-row">
              <div class="form-group col-md-6">
                <input
                  type="text"
                  class="form-control"
                  placeholder="Full Name"
                  v-model="userData.name"
                />
              </div>
              <div class="form-group col-md-6">
                <input
                  type="text"
                  class="form-control"
                  placeholder="Username"
                  v-model="userData.username"
                />
              </div>
            </div>
            <div class="form-row">
              <div class="form-group col-md-6">
                <input
                  type="text"
                  class="form-control"
                  placeholder="Email"
                  v-model="userData.email"
                />
              </div>
              <div class="form-group col-md-6">
                <input
                  type="text"
                  class="form-control"
                  placeholder="Phone"
                  v-model="userData.phone"
                />
              </div>
            </div>
            <div class="form-row">
              <div class="form-group col-md-12">
                <input
                  type="text"
                  class="form-control"
                  placeholder="Website"
                  v-model="userData.website"
                />
              </div>
            </div>
            <div class="form-row">
              <div class="form-group col-md-4">
                <input
                  type="text"
                  class="form-control"
                  placeholder="Company Name"
                  v-model="userData.company.name"
                />
              </div>
              <div class="form-group col-md-4">
                <input
                  type="text"
                  class="form-control"
                  placeholder="Company Catch Phrase"
                  v-model="userData.company.catchPhrase"
                />
              </div>
              <div class="form-group col-md-4">
                <input
                  type="text"
                  class="form-control"
                  placeholder="Company BS"
                  v-model="userData.company.bs"
                />
              </div>
            </div>
            <div class="form-row">
              <div class="form-group col-md-3">
                <input
                  type="text"
                  class="form-control"
                  placeholder="Street"
                  v-model="userData.address.street"
                />
              </div>
              <div class="form-group col-md-3">
                <input
                  type="text"
                  class="form-control"
                  placeholder="Suite"
                  v-model="userData.address.suite"
                />
              </div>
              <div class="form-group col-md-3">
                <input
                  type="text"
                  class="form-control"
                  placeholder="City"
                  v-model="userData.address.city"
                />
              </div>
              <div class="form-group col-md-3">
                <input
                  type="text"
                  class="form-control"
                  placeholder="Zip"
                  v-model="userData.address.zipcode"
                />
              </div>
            </div>
          </div>
          <div class="modal-footer">
            <button class="btn btn-success" @click="saveUser()">
              Save Changes
              <i class="fa fa-save"></i>
            </button>
            <button class="btn btn-secondary" data-dismiss="modal">Close</button>
          </div>
        </div>
      </div>
    </div>
    <div class="modal fade" id="userDataModal" tabindex="-1" role="dialog">
      <div class="modal-dialog modal-dialog-centered" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">User Data</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            Name
            <i class="fa fa-user"></i> :
            <strong>{{userData.name}}</strong>
            <br />Username
            <i class="fa fa-user"></i> :
            <strong>{{userData.username}}</strong>
            <br />Email :
            <i class="fa fa-envelope"></i> :
            <strong>{{userData.email}}</strong>
            <br />Website
            <i class="fa fa-globe"></i> :
            <a v-bind:href="userData.website">
              <strong>{{userData.website}}</strong>
            </a>
            <br />Phone Number
            <i class="fa fa-phone"></i> :
            <strong>{{userData.phone}}</strong>
            <br />ZipCode
            <i class="fa fa-map-pin"></i> :
            <strong>{{userData.address.zipcode}},</strong>
            <br />Address
            <i class="fa fa-sticky-note"></i>
            :
            {{userData.address.street}} St, {{userData.address.suite}}, {{userData.address.city}}
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style lang="css" scoped>
@import "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.css";
</style>
<script>
import axios from "axios";
import $ from "jquery";
import swal from "sweetalert";
import "../src/assets/datatable.js";
import "../src/assets/datatable.css";
export default {
  name: "app",
  data() {
    return {
      users: {},
      userData: { address: {}, company: {} },
      userID: null,
      msg: "",
      action: "",
      loader: "block"
    };
  },
  methods: {
    getUsers() {
      axios
        .get("https://jsonplaceholder.typicode.com/users")
        .then(res => {
          this.users = res.data;
        })
        .catch(err => {
          swal("Problem Occured", "Error loading data", "error");
        });
    },
    userInfo(id) {
      $("#cover-spin").show();
      axios
        .get(`https://jsonplaceholder.typicode.com/users/${id}`)
        .then(res => {
          this.userData = res.data;
          $("#cover-spin").hide();
          $("#userDataModal").modal("show");
        })
        .catch(err => {
          swal(
            "Error",
            "Problem Occurred loading data, Try again Later",
            "error"
          );
        });
    },
    newUserModal() {
      this.msg = "";
      this.userData = { address: {}, company: {} };
      this.action = "NEW_USER";
      $("#userModal").modal("show");
    },
    editUserModal(user) {
      this.msg = "";
      this.userID = user.id;
      this.userData = user;
      this.action = "EDIT_USER";
      $("#userModal").modal("show");
    },
    deleteUser(id, name) {
      swal({
        title: "Are you sure ?",
        text: `Delete all data relating to ${name}`,
        icon: "warning",
        buttons: {
          cancel: {
            text: "Cancel",
            value: null,
            visible: true,
            closeModal: true,
            className: "btn btn-default"
          },
          confirm: {
            text: "Yes Delete",
            value: "delete",
            visible: true,
            className: "btn btn-danger"
          }
        },
        closeOnClickOutside: false
      }).then(btn => {
        if (btn == "delete") {
          this.users = this.users.filter(val => {
            return val.id !== id;
          });
          //The fetch function does not return any data.
          //So I simulated the delete by removing it from the 'users' array.
          //The normal ideal code is found below
          $("#cover-spin").show();
          axios({
            method: "DELETE",
            url: `https://jsonplaceholder.typicode.com/users/${id}`
          }).then(res => {
            $("#cover-spin").hide();
            swal("Done", `${name} record deleted`, "success");
          });
        }
      });
    },
    saveUser() {
      if (this.validateUser()) {
        $("#cover-spin").show();
        $("#userModal").modal("hide");
        if (this.action == "NEW_USER") {
          axios
            .post(
              "https://jsonplaceholder.typicode.com/users",
              JSON.stringify(this.userData),
              {
                headers: {
                  "Content-type": "application/json; charset=UTF-8"
                }
              }
            )
            .then(res => {
              $("#cover-spin").hide();
              this.users.push(res.data);
              swal("Done", "New User Added", "success");
            })
            .catch(err => {
              $("#cover-spin").hide();
              swal("OOps", "Error encoutered", "failed");
              console.log(err);
            });
        }

        if (this.action == "EDIT_USER") {
          axios
            .put(
              `https://jsonplaceholder.typicode.com/posts/${this.userID}`,
              JSON.stringify(this.userData),
              {
                headers: {
                  "Content-type": "application/json; charset=UTF-8"
                }
              }
            )
            .then(res => {
              $("#cover-spin").hide();
              swal("Done", "User Record Updated", "success");
            })
            .catch(err => {
              $("#cover-spin").hide();
              swal("OOps", "Error encoutered", "failed");
              console.log(err);
            });
        }
      } else {
        this.msg = msg;
      }
    },
    validateUser() {
      let kase = true;
      let msg = "";

      if (
        !(
          this.userData.name &&
          /^([a-zA-Z]+[a-zA-Z\ \-\'])+$/.test(this.userData.name)
        )
      ) {
        kase &= false;
        msg += "Enter a valid full name(firstname lastname) <br/>";
      }

      if (
        !(
          this.userData.username &&
          /^[A-Za-z0-9]+(?:[_-][A-Za-z0-9]+)*$/.test(this.userData.username)
        )
      ) {
        kase &= false;
        msg += "Enter a valid username <br/>";
      }

      if (
        !/^[a-zA-Z0-9.!#$%&’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/.test(
          this.userData.email
        )
      ) {
        kase &= false;
        msg += "Enter a valid email address <br/>";
      }

      if (!/^(\(?\+?[0-9]*\)?)?[0-9_\- \(\)]*$/.test(this.userData.phone)) {
        msg += "Enter a valid phone number <br/>";
        kase &= false;
      }

      if (
        !/^(?:http(s)?:\/\/)?[\w.-]+(?:\.[\w\.-]+)+[\w\-\._~:/?#[\]@!\$&'\(\)\*\+,;=.]+$/.test(
          this.userData.website
        )
      ) {
        msg += "Enter a valid website <br/>";
        kase &= false;
      }

      if (!kase) {
        this.msg = msg;
      }

      return kase;
    }
  },
  mounted() {
    this.getUsers();
  },
  updated() {
    $("#table").DataTable({
      lengthChange: false,
      pageLength: 5
    });
  }
};
</script>

