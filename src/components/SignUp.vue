<template>
  <form @submit.prevent="submit">
    <label for="">Email</label>
    <input type="email" v-model="email" />

    <label for="">Password</label>
    <input type="password" v-model="password" />
    <p v-if="errorMsg" class="text-danger">{{errorMsg}}</p>

    <label for="">Roles</label>
    <select v-model="roles">
      <option value="developer">Depeloper</option>
      <option value="designer">Designer</option>
    </select>
    <div>
        <label for="">Skills</label>
        <input type="text" @keyup.enter="addSkill" v-model="skill">
    </div>
    <div>

    </div>
   <div v-for="skill in skills" :key="skill">
       <p>{{skill}}<span class="cross" @click="deleteSkill(skill)">&#10060;</span></p><br>
   </div>
    <div>
        <input type="checkbox" v-model="accept">
        <label for="">Accept terms and Condition</label>
    </div>
    <div class="col-md-12 text-center">
        <button class="mx-auto btn btn-primary">Create Account</button>
    </div>
  </form>
 


</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      roles:"",
      accept:true,
      skills:[],
      skill:"",
      errorMsg:""
    }
  },
  methods:{
      addSkill(){
         if (this.skill) {
             this.skills.push(this.skill);
             this.skill=""
         }
      },
      deleteSkill(skill){
         this.skills = this.skills.filter(loopSkill=>{
            return loopSkill != skill;
         })
      },
      submit(){
          console.log("submit");
            if (this.password.length<8) {
                this.errorMsg="Password must be at least 8 characters"
            }
      }
  }
};
</script>

<style>
body{
    background-color: #aaa;
}
form{
  max-width: 420px;
  margin: 100px auto;
  background: rgb(255, 255, 255);
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label{
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: boder-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
input[type="checkbox"]{
        display: inline-block;
        width: 16px;
        margin: 0 5px 0 0;
        position: relative;
        top: 3px;
}
.cross{
    cursor: pointer;
}
</style>
