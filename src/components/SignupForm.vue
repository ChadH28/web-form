<template>
<!-- wrap everything in a div container -->
  <div>
    <form>
      <!-- input fields -->
      <label>User:</label>
      <input type="text" v-model="name" required />

      <label>Email:</label>
      <input type="email" v-model="email" required />

      <label>Password:</label>
      <input type="password" v-model="password" required />
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
    </form>

    <p>
      User: {{ name }} <br />
      Email: {{ email }} <br />
      Password: {{ password }} <br />
      Role: {{ role }} <br />
      Terms: {{ terms }} <br />
      Traits: {{ traits }} <br />
    </p>

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
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill) {
        this.skills.push(this.tempSkill);
        this.tempSkill = "";
      }
    },
  },
};
</script>

<style>
form {
  max-width: 450px;
  width: 400px;
  margin: 30px auto;
  background: white;
  box-sizing: border-box;
  text-align: left;
  padding: 40px;
  border-radius: 12px;
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
</style>