<template>
  <div>
    <h2>{{ msg }}</h2>
    <h1><p style="color: greenyellow;">HelloWorld.</p></h1>

    <!-- Your form with name, email, and password fields -->
    <form @submit.prevent="submitForm">
      <label for="name">Name:</label>
      <input type="text" id="name" v-model="name" required>

      <label for="email">Email:</label>
      <input type="email" id="email" v-model="email" required>

      <label for="password">Password:</label>
      <input type="password" id="password" v-model="password" required>

      <button type="submit">Submit</button>
    </form>

    <!-- Display the submitted data -->
    <div v-if="submitted">
      <h3>Submitted Data:</h3>
      <p><strong>Name:</strong> {{ submittedData.name }}</p>
      <p><strong>Email:</strong> {{ submittedData.email }}</p>
      <p><strong>Password:</strong> {{ submittedData.password }}</p>
    </div>

    <button @click="getData">Get Data</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      msg: 'Welcome All',
      name: '',
      email: '',
      password: '',
      submitted: false, // Track if the form has been submitted
      submittedData: {}, // Store the submitted data
    };
  },
  methods: {
    async submitForm() {
      // Do something with the submitted data
      console.log('Name:', this.name);
      console.log('Email:', this.email);
      console.log('Password:', this.password);

      // Send data to an endpoint using the fetch API
      try {
        const response = await fetch('http://127.0.0.1:5000/save', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            name: this.name,
            email: this.email,
            password: this.password,
          }),
        });

        if (response.ok) {
          console.log('Data sent successfully!');
          // Set submitted to true to display the submitted data
          this.submitted = true;
          // Store the submitted data
          this.submittedData = {
            name: this.name,
            email: this.email,
            password: this.password,
          };
        } else {
          console.error('Failed to send data.');
        }
      } catch (error) {
        console.error('Error:', error);
      }
    },
    async getData() {
      // Fetch data from the server
      try {
        const response = await fetch('http://127.0.0.1:5000/data');

        if (response.ok) {
          const data = await response.json();
          console.log('Received Data:', data);

          // Display the received data on the webpage
          this.submittedData = data;
        } else {
          console.error('Failed to fetch data.');
        }
      } catch (error) {
        console.error('Error:', error);
      }
    },
  },
};
</script>

<style scoped>
/* Your component-specific styles */
</style>
