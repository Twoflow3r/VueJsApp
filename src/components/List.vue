<template>
<div class="wrap">
  <div class="row">
 <div class="input-field col s4 ">
        <label for="query">
        </label>
        <i class="material-icons prefix">search</i>
      <input v-model="query" placeholder="Кого вы ищете?" class="form-control">
    </div>
    <!--
    <div class="input-field col s1 offset-s7">
       <input v-model="name" placeholder="Кого вы ищете?" class="form-control">
        <input v-model="phone" placeholder="Кого вы ищете?" class="form-control">
         <input v-model="email" placeholder="Кого вы ищете?" class="form-control">
      <button class="btn-floating btn-large waves-effect waves-light red" @click="createContact()"><i class="material-icons left">add</i></button>
    </div>
    -->
  </div>

  <table class="table centered">
    <tr>
      <th>id</th>
      <th><button class="waves-effect waves-light btn-small" @click="sort('name')"><i class="material-icons left">person</i>Имя</button> </th>
      <th><button class="waves-effect waves-light btn-small" @click="sort('phone')"><i class="material-icons left">phone</i>Телефон</button></th>
      <th><button class="waves-effect waves-light btn-small" @click="sort('email')"><i class="material-icons left">email</i>Email</button></th>
      <th>Удалить</th>
    </tr>
    <tr v-for="(contact, index) in sortedList" :key="index" is="tr"  :sortedList="sortedList">
       <td>{{contact.index}}</td>
      <td>{{contact.name | capitalize }}</td>
      <td>{{contact.phone}}</td>
       <td>{{contact.email}}</td>
       <button class="waves-effect waves-darken-3 red  btn-small" v-on:click="removeElement(contact)"><i class="material-icons">delete_forever</i></button>
    </tr>
  </table>

  <ul class="pagination">
    <li class="waves-effect"><a @click="prevPage"><i class="material-icons">chevron_left</i></a></li>
    <li class="waves-effect"><a  @click="nextPage"><i class="material-icons">chevron_right</i></a></li>
  </ul>
<!--
 <div class="row">
  <div class="input-field ">
    <label>Имя</label>
    <input type="text" class="form-control" v-model="newContact.name" >
  </div>

  <div class="input-field ">
    <label>Телефон</label>
    <input type="name" class="form-control" v-model="newContact.phone" >
  </div>
  <div class="input-field ">
    <label>email</label>
    <input type="name" class="form-control" v-model="newContact.email" >
  </div>
  <div class="input-field ">

 </div>
-->
 <div class="row">
    <form class="col s12">
      <div class="row">
        <div class="input-field col s12">
          <input id="text" type="text" required class="validate">
          <label for="Имя">Имя</label>
          <span class="helper-text" data-error="wrong" data-success="right" v-model="newContact.name"></span>
        </div>

        <div class="input-field col s12">
          <input id="email" type="text" required class="validate">
          <label for="email">phone</label>
          <span class="helper-text" data-error="wrong" data-success="right" v-model="newContact.phone"></span>
        </div>

        <div class="input-field col s12">
          <input id="email" type="email" required class="validate">
          <label for="email">Email</label>
          <span class="helper-text" data-error="wrong" data-success="right" v-model="newContact.email"></span>
        </div>
      </div>
       <button class="btn-floating btn-large waves-effect waves-light red" v-on:click="addContact()"><i class="material-icons left">add</i></button>
    </form>
  </div>
 </div>
</div>
</template>

<script>
export default {
 data: function () {
  return {
    order: 1,
    sortParam: '',
    currentSort:'name',
    currentSortDir:'asc',
    pageSize:5,
    currentPage:1,
    query: '',
    newContact: {}
  }
},
methods:{
  sort:function(s) {
    //if s == current sort, reverse
    if(s === this.currentSort) {
      this.currentSortDir = this.currentSortDir==='asc'?'desc':'asc';
    }
    this.currentSort = s;
  },
    nextPage:function() {
      if((this.currentPage*this.pageSize) < this.contacts.length) this.currentPage++;
    },
    prevPage:function() {
      if(this.currentPage > 1) this.currentPage--;
    },
    filterByName : function(contacts) {
      if (this.query.length === 0) {
        return true;
      }
      return  (contacts.name.toLowerCase().indexOf(this.query.toLowerCase()) > -1);
    },
    removeElement : function (contact) {
      var index = this.contacts.indexOf(contact);
       this.contacts.splice(index, 1)
      },
      createContact: function () {
         var newContact = {
            name: '',
            phone: '',
            email: ''
        };
       this.contacts.push(newContact);
     },
     addContact: function() {
      this.contacts.push(this.newContact);
      this.newContact = {};
    }
    
},
computed:{
  sortedList :function() {
    return this.contacts.sort((a,b) => {
      let modifier = 1;
      if(this.currentSortDir === 'desc') modifier = -1;
      if(a[this.currentSort] < b[this.currentSort]) return -1 * modifier;
      if(a[this.currentSort] > b[this.currentSort]) return 1 * modifier;
      return 0;
    })
      .filter((row, index) => {
        let start = (this.currentPage-1)*this.pageSize;
        let end = this.currentPage*this.pageSize;
        if(index >= start && index < end) return true;
      }) 
      .filter(this.filterByName);
    }
  },
  props: ["contacts"],
  filters: {
  capitalize: function (value) {
    if (!value) return ''
    value = value.toString()
    return value.charAt(0).toUpperCase() + value.slice(1)
  }
}
}


</script>

<style>
th, td{
  text-align: center;
  padding: 1rem;
}

</style>
