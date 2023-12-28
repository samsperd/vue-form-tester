<template>
  <form @submit.prevent="handleSubmit">
    <label>
        Email
    </label>
    <input type="email" v-model="email" required />

    <label>
        Password
    </label>
    <input type="password" v-model="password" required />
    <div class="error" v-if="passwordError" >{{ passwordError }}</div>

    <label>Role:</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup="addSkill">
    <div class="pill" v-for="skill in skills" :key="skill">
      <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>

    <div class="terms">
      <input type="checkbox" v-model="terms" required>
      <label>Accept terms and conditions</label>
    </div>

    <div class="submit">
      <button>Create An Account</button>
    </div>
  </form>

  <hr>
  <div class="">
    <input type="checkbox" value="mike" v-model="names">
    <label>Mike</label>
  </div>
  <div class="">
    <input type="checkbox" value="tunde" v-model="names">
    <label>Tunde</label>
  </div>
  <div class="">
    <input type="checkbox" value="ike" v-model="names">
    <label>Ike</label>
  </div>

  <p>Email: {{ email }}</p>
  <p>Password {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms Accepted: {{ terms }}</p>
  <p>Names: {{ names }}</p>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      role: 'designer',
      terms: false,
      names: [],
      tempSkill: '',
      skills: [],
      passwordError: ''
    }
  },
  methods: {
    addSkill(e) {
      if (e.key === ',' && this.tempSkill) {
        const commaIndex = this.tempSkill.lastIndexOf(",")
        const word = this.tempSkill.substring(0, commaIndex).trim()

        if (!this.skills.includes(word)) {
          this.skills.push(word)
        }
        this.tempSkill = ''
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item
      })
    },

    handleSubmit() {

      //Validate Password
      this.passwordError = this.password.length > 5 ? 
      '' : 'Password must be at least 6 characters long'
      
      if (!this.passwordError) {
        console.log("Form Submitted");
        console.log("Email", this.email);
        console.log("Password", this.password);
        console.log("Role", this.role);
        console.log("Skills", this.skills);
        console.log("Terms Accepted", this.terms);

      }
    }
  },

}
</script>

<style>
form {
    max-width: 420px;
    margin: 30px auto;
    text-align: left;
    padding: 40px;
    background: white;
    border-radius: 10px;
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

input, select {
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

.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}

.submit {
  text-align: center;
}

button {
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
}

.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
</style>