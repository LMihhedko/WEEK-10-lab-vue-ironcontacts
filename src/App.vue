<script setup>
import contacts from "./contacts.json";

import { ref } from "vue";

let fiveContacts = ref(contacts.slice(0, 5));

console.log(fiveContacts);

function addRandomContact() {
  let randomContact = contacts[Math.floor(Math.random() * contacts.length)];

  if (fiveContacts.value.includes(randomContact)) {
    return;
  } else {
    fiveContacts.value.push(randomContact);
  }
}

function sortByPopularity() {
  fiveContacts.value.sort((a, b) => b.popularity - a.popularity);
  return fiveContacts;
}

function sortByName() {
  fiveContacts.value.sort((a, b) => a.name.localeCompare(b.name));
  return fiveContacts;
}

function deleteContact(id) {
  console.log(id);

  fiveContacts.value.forEach((contact, index) => {
    if (contact.id === id) {
      fiveContacts.value.splice(index, 1);
      return fiveContacts;
    }
  });
}
</script>

<template>
  <div id="app">
    <div id="header">
      <p>Iron Contacts</p>
      <button class="btn-m" @click="addRandomContact()">
        Add Random Contact
      </button>
      <button class="btn-m" @click="sortByPopularity()">
        Sort by popularity
      </button>
      <button class="btn-m" @click="sortByName()">Sort by name</button>
    </div>
    <table>
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won an Oscar</th>
        <th>Won an Emmy</th>
        <th>Actions</th>
      </tr>
      <tr v-for="contact in fiveContacts">
        <td><img :src="contact.pictureUrl" /></td>
        <td>{{ contact.name }}</td>
        <td>{{ contact.popularity.toFixed(2) }}</td>
        <td v-if="contact.wonOscar">🏆</td>
        <td v-else="contact.wonOscar"></td>
        <td v-if="contact.wonEmmy">🏆</td>
        <td v-else="contact.wonEmmy"></td>
        <td><button @click="deleteContact(contact.id)">Delete</button></td>
      </tr>
    </table>
  </div>
</template>

<style>
p {
  font-size: 2rem;
  font-weight: 700;
}

img {
  width: 80px;
}

table {
  text-align: center;
  border-spacing: 20px;
  border-spacing: 20px;
  margin-left: auto;
  margin-right: auto;
}

#header {
  text-align: center;
}

.btn-m {
  margin-left: 10px;
}
</style>
