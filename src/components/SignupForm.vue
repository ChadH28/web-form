<template>
  <!-- wrap everything in a div container -->
  <div>
    <p id="alert"></p>
    <form @submit.prevent="handleSubmit">
      <!-- input fields -->
      <label>User:</label>
      <input type="text" v-model="name" required />

      <label>Email:</label>
      <input type="email" v-model="email" required />

      <label>Password:</label>
      <input type="password" v-model="password" required />
      <div v-if="passwordError" id="error">
        {{passwordError}}
      </div>
      <!-- multiple checkbox -->
      <div>
        <input v-model="traits" type="checkbox" value="Analytical" />
        <label>Analytical</label>
      </div>

      <div>
        <input v-model="traits" type="checkbox" value="Book-worm" />
        <label>Book-worm</label>
      </div>

      <div>
        <input v-model="traits" type="checkbox" value="Workhorse" />
        <label>Workhorse</label>
      </div>
      <!-- select box -->
      <label>Role:</label><br />
      <select v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
      </select>
      <!-- checkbox -->
      <div class="terms">
        <input v-model="terms" type="checkbox" required />
        <label>Accept terms and conditions</label>
      </div>

      <label>Skills:</label>
      <input type="text" v-model="tempSkill" @keyup="addSkill" />
      <!-- looping through skills list  -->
      <!-- :key must be unique -->
      <div v-for="skill in skills" :key="skill" class="badge">
        <span @click="deleteSkill(skill)">{{skill}}</span>
      </div>

      <div class="submit">
        <button>Create an account </button>
      </div>
    </form>

    <div class="output">
      <h1>Output</h1>
    <p>
      User: {{ name }} <br />
      Email: {{ email }} <br />
      Password: {{ password }} <br />
      Role: {{ role }} <br />
      Terms: {{ terms }} <br />
      Traits: {{ traits }} <br />
    </p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      name: "",
      role: "",
      terms: false,
      traits: [],
      tempSkill: "",
      skills: [],
      passwordError: ''
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "Enter" && this.tempSkill ) {
        // statement checks whether if theres duplicates or not
        if(!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
        }
        this.tempSkill = "";
      }
    },
    deleteSkill(skill) {
        this.skills = this.skills.filter((i) => {
          return skill !== i
        })
    },
  handleSubmit() {
    document.getElementById('alert').innerHTML = 'form submitted'
    // password validation
    this.passwordError = this.password.length > 5 ? '' : 'Must be atleast 5 characters long' 
  
    if(!this.passwordError) {
      console.log('email', this.email)
      console.log('password', this.password)
      console.log('role', this.role)
      console.log('skills', this.skills)
      console.log('terms accepted', this.terms)
    }
  }
  },
};
</script>

<style>
form,
.output {
  max-width: 450px;
  width: 400px;
  margin: 30px auto;
  background: white;
  box-sizing: border-box;
  text-align: left;
  padding: 40px;
  border-radius: 12px;
}

.output p{
  padding-bottom:20px;
}

label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}

input,
select,
options {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}

input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}

.badge {
  padding: 10px;
  margin: 10px 5px;
  background: cadetblue;
  border: none;
  border-radius: 25px ;
  cursor: pointer;
  font-weight: bold;
  box-sizing: border-box;
  font-size: 12px; 
  display: inline-block;
}

.badge:hover{
  opacity: 0.8
}

button{
  background: cadetblue;
  border: none;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 25px;
  cursor: pointer;
}
button:hover{
  opacity: 0.8;
}

.submit{
  text-align: center;
  margin: 10px auto;
}

#alert{
  background: chartreuse;
  padding: 20px 10px;
  margin: 10px auto;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
  font-size: 20px;
  color:white;
}

#error{
    background: rgba(255, 99, 71, 0.6);
    color: white;
    padding: 10px 5px;
    font-weight: bold;
    text-align: center;
}

</style>