<template>
  <section class="container">
    <h1>Add New Contact</h1>

    <form @submit.prevent="saveContact">

      <div class="field">
        <label for="" class="label">First Name</label>
        <div class="control">
          <input type="text" class="input" placeholder="First Name" v-model="firstname" required>
        </div>
      </div>

      <div class="field">
        <label for="" class="label">Last Name</label>
        <div class="control">
          <input type="text" class="input" placeholder="Last Name" v-model="lastname" required>
        </div>
      </div>

      <div class="field">
        <label for="" class="label">Email Address</label>
        <div class="control">
          <input type="email" class="input" placeholder="Email Address" v-model="emailaddress" required>
        </div>
      </div>

      <div class="field">
        <label for="" class="label">Phone Number</label>
        <div class="control">
          <input type="text" class="input" placeholder="Phone Number" v-model="phonenumber" required>
        </div>
      </div>

      <div class="field">
        <div class="control">
          <button type="submit" class="button is-link">Submit</button>
        </div>
      </div>

    </form>
  </section>

</template>

<script>
  import db from '../../config/firebaseInit'
  export default {
    name: 'new-contact',
    data () {
      return {
        firstname: null,
        lastname: null,
        emailaddress: null,
        phonenumber: null
      }
    },
    methods: {
      saveContact () {
        db.collection('contacts').add({
          firstname: this.firstname,
          lastname: this.lastname,
          emailaddress: this.emailaddress,
          phonenumber: this.phonenumber,
          slug: this.generateUUID()
        })
          .then(function (docRef) {
            console.log('Document written with ID: ', docRef.id)
          })
          .catch(function (error) {
            console.error('Error adding document: ', error)
          })
      },
      generateUUID () {
        let date = new Date().getTime()
        let uuid = 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function (c) {
          let random = (date + Math.random() * 16) % 16 | 0
          date = Math.floor(date / 16)
          return (c === 'x' ? random : (random & 0x3 | 0x8)).toString(16)
        })
        return uuid
      }
    }
  }
</script>

<style>

  section{
    height: 100vh;
  }

  h2 {
    font-size: 30px;
    margin: 30px 0;
  }

  .input {
    height: 40px;
  }

</style>
