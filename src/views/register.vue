<template>
    <div class="register flex relative h-screen justify-center">
        <div class="w-1/2 h-full text-red-500 justify-center flex items-center">
            <form @submit.prevent="register" class="form !bg-slate-200">
            <p class="title">Register </p>
        <div class="flex">

        <label>
            <input required="" v-model="Firstname" id="Firstname" placeholder="" type="text" class="input !bg-slate-200">
            <span>Firstname</span>
        </label>

        <label>
            <input required="" id="Lastname" placeholder="" type="text" class="input !bg-slate-200">
            <span>Lastname</span>
        </label>
    </div>  
            
    <label>
        <input required="" id="email" placeholder="" type="email" class="input !bg-slate-200">
        <span>Email</span>
    </label> 
    <label>
        <input required="" id="number" placeholder="" type="number" maxlength="11" class="input !bg-slate-200">
        <span>number</span>
    </label> 
        
    <label>
        <input required="" id="password" v-model="Password"  placeholder="" type="password" class="input !bg-slate-200">
        <span id="passwordt">Password</span>
    </label>
    <label>
        <input required="" id="confirmPassword" v-model="Confirm_password" placeholder="" type="password" class="input !bg-slate-200">
        <span id="confirmPasswordt">Confirm password</span>
    </label>
    <div id="error_text"></div>
    <button class="submit">Submit</button>
    <p class="signin">Already have an acount ?<router-link to="/Login">Login</router-link></p>
</form>
        </div>
        <div class="w-auto h-full flex justify-center">
            <img class="h-full w-full md:w-auto" src="../../public/img/login.jpg" alt="">
        </div>
    </div>
</template>

<script>
import $ from 'jquery'
import axios from 'axios'
export default {
    data(){
       return{
        Firstname:null,
        Lastname:null,
        Email:null,
        Password:'',
        Confirm_password:'',
        error:true
       } 
    },
    methods:{
        async register(){
            if(!this.error){
            try {
            let search_data = (await axios.get(`https://pcc.co.ir/api/register?name=${this.Firstname}&fname=${this.Lastname}&email=${this.Email}&number=0990220354dd01&password=${this.Password}`)) 
            console.log(search_data)
            // search_data = search_data.data
            // if(search_data.next != null){
            //     this.next2 = true
            //     this.next = search_data.next
            // }else{
            //     this.next2 = false
            // }
            // search_data = search_data.results
            // this.news_first = search_data.slice(0,5);
            // this.news_end = search_data.slice(5);
            // console.log(this.news_first)
            // console.log(this.news_end)
  
            } catch (error) {
        console.error(error);
            } 
            }
            else{
                console.log("error")
            }
        
        }
    },
    watch: {
        Password(newValue) {
            $("#confirmPasswordt").addClass("!text-red-500")
            $("#passwordt").addClass("!text-red-500")
            $("#error_text").html("password is not same to confirmPassword")
            this.error = true
            if(this.Password == this.Confirm_password ){
                $("#confirmPasswordt").removeClass("!text-red-500")
                $("#passwordt").removeClass("!text-red-500")
                this.error = false
                $("#error_text").html("")

            }
    },
        Confirm_password(newValue) {
            $("#confirmPasswordt").addClass("!text-red-500")
            $("#passwordt").addClass("!text-red-500")
            $("#error_text").html("password is not same to confirmPassword")
            this.error = true
            if(this.Password == this.Confirm_password ){
                $("#confirmPasswordt").removeClass("!text-red-500")
                $("#passwordt").removeClass("!text-red-500")
                this.error = false
                $("#error_text").html("")

            }
    },
  },
        
}
</script>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  max-width: 350px;
  background-color: #fff;
  padding: 20px;
  border-radius: 20px;
  position: relative;
}

.title {
  font-size: 28px;
  color: royalblue;
  font-weight: 600;
  letter-spacing: -1px;
  position: relative;
  display: flex;
  align-items: center;
  padding-left: 30px;
}

.title::before,.title::after {
  position: absolute;
  content: "";
  height: 16px;
  width: 16px;
  border-radius: 50%;
  left: 0px;
  background-color: royalblue;
}

.title::before {
  width: 18px;
  height: 18px;
  background-color: royalblue;
}

.title::after {
  width: 18px;
  height: 18px;
  animation: pulse 1s linear infinite;
}

.message, .signin {
  color: rgba(88, 87, 87, 0.822);
  font-size: 14px;
}

.signin {
  text-align: center;
}

.signin a {
  color: royalblue;
}

.signin a:hover {
  text-decoration: underline royalblue;
}

.flex {
  display: flex;
  width: 100%;
  gap: 6px;
}

.form label {
  position: relative;
}

.form label .input {
  width: 100%;
  padding: 10px 10px 20px 10px;
  outline: 0;
  border: 1px solid rgba(105, 105, 105, 0.397);
  border-radius: 10px;
}

.form label .input + span {
  position: absolute;
  left: 10px;
  top: 15px;
  color: grey;
  font-size: 0.9em;
  cursor: text;
  transition: 0.3s ease;
}

.form label .input:placeholder-shown + span {
  top: 15px;
  font-size: 0.9em;
}

.form label .input:focus + span,.form label .input:valid + span {
  top: 30px;
  font-size: 0.7em;
  font-weight: 600;
}

.form label .input:valid + span {
  color: rgb(0, 81, 162);
}
.form label .input:valid {
  color: green;
}

.submit {
  border: none;
  outline: none;
  background-color: royalblue;
  padding: 10px;
  border-radius: 10px;
  color: #fff;
  font-size: 16px;
  transform: .3s ease;
}

.submit:hover {
  background-color: rgb(56, 90, 194);
}

@keyframes pulse {
  from {
    transform: scale(0.9);
    opacity: 1;
  }

  to {
    transform: scale(1.8);
    opacity: 0;
  }
}
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
}
</style>