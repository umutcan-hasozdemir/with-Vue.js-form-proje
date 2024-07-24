<template>
    <div>
      <h2>Form Projesi</h2>
      <form @submit.prevent="handleSubmit">
        <label>Email:</label>
        <input type="email" v-model="email" required />
  
        <label>Şifre:</label>
        <input type="password" v-model="password" required />
        <div v-if="passwordEror" class="passworderor">
            {{passwordEror}}
        </div>
  
        <label>Cinsiyet:</label>
  
        <select v-model="gender">
          <option value="male">Erkek</option>
          <option value="female">Kadın</option>
        </select>
  
        <label>Bildiğiniz diller</label>
        <input type="text" v-model="skill" @keyup.alt="addSkill($event)" />
        <div v-for="skillItem in skills" :key="skillItem" class="skillItem">
          <span @click="deleteSkill(skillItem)">{{ skillItem }} </span>
        </div>
  
        <div class="term">
          <input class="termInput" type="checkbox" v-model="term" required />
          <label>Kullanım koşullarını kabul ediniz</label>
        </div>
  
        <div class="btndiv">
          <button>Kaydol</button>
        </div>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        email: "eryvfjdn@gmail.com",
        password: "",
        gender: "male",
        term: false,
        skills: [],
        skill: "",
        passwordEror: false,
      };
    },
    methods: {
      addSkill(e) {
        if (e.key === "," && this.skill) {
          if (!this.skills.includes(this.skill)) {
            this.skills.push(this.skill);
          }
          this.skill = "";
        }
      },
      deleteSkill(skill) {
        this.skills = this.skills.filter((item) => {
          return skill !== item;
        });
      },
        handleSubmit() {
            this.passwordEror = this.password.length > 5 ? '' : 'Minimum 5 karakter olmalıdır'  
       console.log('Email' , this.email);
       console.log('Password' , this.password);
       console.log('Gender' , this.gender);
       console.log('Term' , this.term);
       console.log('Skills' , this.skills);
        },
    },
  };
  </script>
  
  <style>
  body {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
  }
  h2 {
    text-align: center;
    margin: 20px 10px 10px 80px;
  }
  form {
    max-width: 450px;
    width: 100%;
    background: antiquewhite;
    padding: 40px;
    border-radius: 20px;
    text-align: left;
    margin: 40px auto;
  }
  input,
  select {
    display: block;
    width: 100%;
    padding: 10px 8px;
    border-radius: 20px;
    border: none;
    outline: none;
  }
  label {
    margin: 15px 10px;
    display: inline-block;
    font-size: 15px;
    font-weight: bold;
    letter-spacing: 2px;
  }
  .termInput {
    width: 16px;
  }
  .term {
    display: flex;
    align-items: center;
  }
  button {
    border: none;
    background: green;
    color: white;
    padding: 10px 20px;
    font-size: 18px;
    border-radius: 20px;
  }
  
  .skillItem {
    background: white;
    margin: 20px 10px;
    display: inline-block;
    padding: 8px 10px;
    border-radius: 20px;
    color: gray;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
  }
  .passworderor {
    color: red;
    margin-top: 10px;
    font-size: 15px;
    font-weight: bold;
    letter-spacing: 1px;
  }
  </style>
  