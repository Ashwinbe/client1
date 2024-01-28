<template>
    <div>
      <h2>{{ msg }}</h2>
      <h1><p style="color: greenyellow;">HelloWorld.</p></h1>
  
      <!-- Display the submitted data -->
      <div>
        <p><strong>Name:</strong> {{ name }}</p>
        <p><strong>Email:</strong> {{ email }}</p>
        <p><strong>Password:</strong> {{ password }}</p>
      </div>
  
      <!-- Button to go back to the form -->
      <router-link to="/">Go back to Form</router-link>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        msg: 'Displaying Submitted Data',
        name: '',
        email: '',
        password: '',
      };
    },
    mounted() {
      // Fetch and display the submitted data (you may replace this with actual data fetching logic)
      this.fetchSubmittedData();
    },
    methods: {
      async fetchSubmittedData() {
        try {
          // Fetch data from an endpoint (replace 'http://127.0.0.1:5000/data' with your actual endpoint)
          const response = await fetch('http://127.0.0.1:5000/data');
          const data = await response.json();
  
          // Assign data to component properties
          this.name = data.name;
          this.email = data.email;
          this.password = data.password;
        } catch (error) {
          console.error('Error fetching data:', error);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  /* Your component-specific styles */
  </style>
  