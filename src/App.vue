<template>
  <div id="app">

  <h1>Add</h1>
  <table>
    <tbody>
      <tr>
        <td>
          <label>Last Name</label><br>
          <input placeholder="Last Name" v-model="addLastName" type="text">
        </td>
        <td>
          <label>First Name</label><br>
          <input placeholder="First Name" v-model="addFirstName" type="text">
        </td>
        <td>
          <label>Birthday</label><br>
          <input placeholder="Birthday" v-model="addUserBirthDay" type="text">
          </td>
        <td>
          <label>Phone</label><br>
          <input placeholder="Phone" v-model="addUserPhone" type="text">
        </td>
        <td>
          <label>E-Mail</label><br>
          <input placeholder="E-Mail" v-model="addUserEmail" type="text">
        </td>
        <td><label></label><br><a class="buttons" v-on:click="add()">ADD</a></td>
      </tr>
    </tbody>
  </table>


  <h1>Users</h1>
  <table>
    <thead>
      <tr>
        <th v-for="column in persons.columns" v-bind:key="column">
          {{column}}
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(person,index) in persons.persons" v-bind:key="person">
        <td>{{index + 1}}</td>
        <td>
          {{person.lname}}
        </td>
        <td>
          {{person.fname}}
        </td>
        <td>
          {{person.datebirth}} years
        </td>
        <td>
          {{person.phone}}
        </td>
        <td>
          {{person.email}}
        </td>
        <td style="width: 18%;">
          <a class="buttons" v-on:click="edit(index)">edit</a>
          <a class="buttons" v-on:click="deleteOne(index)">delete</a>
        </td>
      </tr>
    </tbody>
  </table>

<h1>Edit</h1>
<table>
  <tbody>
    <tr>
        <td>
          <label>Last Name</label><br>
          <input placeholder="Last Name" v-model="lastName" type="text">
        </td>
        <td>
          <label>First Name</label><br>
          <input placeholder="First Name" v-model="firstName" type="text">
        </td>
        <td>
          <label>Birthday</label><br>
          <input placeholder="Birthday" v-model="userBirthDay" type="text">
        </td>
        <td>
          <label>Phone</label><br>
          <input placeholder="Phone" v-model="userPhone" type="text">
        </td>
        <td>
          <label>E-Mail</label><br>
          <input placeholder="E-Mail" v-model="userEmail" type="text">
        </td>
        <td><label></label><br><a class="buttons" v-on:click="update(index)">Update</a></td>
      </tr>
    </tbody>
  </table>


</div>


</template>

<script>
import users from "./assets/users.json";

export default {
  name: 'app',
  data(){
    return{
        lastName: "",
        firstName: "",
        userBirthDay: "",
        userPhone: "",
        userEmail: "",
        updateUser: {
          "lname": "",
          "fname": "",
          "datebirth": undefined,
          "phone": "",
          "email": ""
        },
        addUser: new Object(),
        id: undefined,
        persons: users
    }
          },
  mounted(){
      this.persons = users;
  },
  methods: {
    deleteOne: function(index) {
      this.persons.persons.splice(index, 1);
    },

    edit: function(index){
      this.lastName = this.persons.persons[index].lname;
      this.firstName = this.persons.persons[index].fname;
      this.userBirthDay = this.persons.persons[index].datebirth;
      this.userPhone = this.persons.persons[index].phone;
      this.userEmail = this.persons.persons[index].email;
      this.id = index;
    },

    update: function(){
      this.updateUser.lname = this.lastName;
      this.updateUser.fname = this.firstName;
      this.updateUser.datebirth = this.userBirthDay;
      this.updateUser.phone = this.userPhone;
      this.updateUser.email = this.userEmail;

      this.persons.persons.splice(this.id, 1, this.updateUser);

      this.lastName = "";
      this.firstName = "";
      this.userBirthDay = undefined;
      this.userPhone = "";
      this.userEmail = "";
    },

    add: function(){
      this.persons.persons.push({
        lname: this.addLastName,
        fname: this.addFirstName,
        datebirth: this.addUserBirthDay,
        phone: this.addUserPhone,
        email: this.addUserEmail
      });

      this.addLastName = "";
      this.addFirstName = "";
      this.addUserBirthDay = undefined;
      this.addUserPhone = "";
      this.addUserEmail = "";
    }
  }
}

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

th {
    text-align: left;
    color: #fff;
    background-color: #706d97;
}
td {
    min-width: 150px;
    color: #696969;
    border-bottom: 1px solid #eee;
}
th, td {
    padding: 5px;
    height: 10px;
}
td:first-child {
    width: 75px;
    min-width: 0;
}
td:last-child {
    width: 40px;
    min-width: 0;
}
tr:nth-child(odd) {
    background-color: #eee;
}

a.buttons{
    background:linear-gradient(to bottom, #FFFFFF, #E6E6E6) #F5F5F5 repeat-x;
    border-color: rgba(0, 0, 0, 0.1) rgba(0, 0, 0, 0.1) #B3B3B3;
    border-radius: 4px;
    border-style: solid;
    border-width: 1px;
    box-shadow: 0 1px 0 rgba(255, 255, 255, 0.2) inset, 0 1px 2px rgba(0, 0, 0, 0.05);
    color: #333333;
        text-decoration:none;
    display:block;
    font-size: 14px;
        width:50px;
    margin: 2px auto;
    padding: 4px 12px;
    text-align: center;
    text-shadow: 0 1px 1px rgba(255, 255, 255, 0.75);
    vertical-align: middle;
  position: relative;
  -webkit-transition-duration: 0.3s;
  transition-duration: 0.3s;
  -webkit-transition-property: -webkit-transform;
  transition-property: transform;
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
  -webkit-transform: translateZ(0);
  -ms-transform: translateZ(0);
  transform: translateZ(0);
  box-shadow: 0 0 1px rgba(0, 0, 0, 0);
}

a.buttons:before {
  pointer-events: none;
  position: absolute;
  z-index: -1;
  content: '';
  top: 100%;
  left: 5%;
  height: 10px;
  width: 90%;
  opacity: 0;
  background: -webkit-radial-gradient(center, ellipse, rgba(0, 0, 0, 0.35) 0%, rgba(0, 0, 0, 0) 80%);
  background: radial-gradient(ellipse at center, rgba(0, 0, 0, 0.35) 0%, rgba(0, 0, 0, 0) 80%);
  -webkit-transition-duration: 0.3s;
  transition-duration: 0.3s;
  -webkit-transition-property: -webkit-transform, opacity;
  transition-property: transform, opacity;
}

a.buttons:hover {
  -webkit-transform: translateY(-5px);
  -ms-transform: translateY(-5px);
  transform: translateY(-5px);
}
a.buttons:hover:before {
  opacity: 1;
  -webkit-transform: translateY(5px);
  -ms-transform: translateY(5px);
  transform: translateY(5px);
}

</style>
