<template>
    <div v-if="!submitted">
 <div class="w-full max-w-sm p-4 bg-white border border-gray-200 rounded-lg shadow sm:p-6 md:p-8 dark:bg-gray-800 dark:border-gray-700">
     <form class="space-y-6" action="#">
         
 
             <h5 class="text-xl font-medium text-gray-900 dark:text-white">Welcome to our Platform.</h5>
         <p>Please enter your details.</p>
 
         <div class="grid gap-6 mb-6 md:grid-cols-2">
         <div>
             <label for="first_name" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">First name</label>
             <input type="text" id="fname" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"  placeholder="John"  v-model="user.fname" name="fname" required>
         </div>
         <div>
             <label for="last_name" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Last name</label>
             <input type="text" id="last_name" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Doe" v-model="user.lname" name="lname" required>
         </div>
         </div>
         <div>
             <label for="email" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Your email</label>
             <input type="email" id="email" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white" placeholder="name@company.com" v-model="user.email" name="email" required>
         </div>
         <div class="grid gap-6 mb-6 md:grid-cols-2">
         <div>
             <label for="password" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Your password</label>
             <input type="password" id="pass" placeholder="••••••••" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white" v-model="user.pass" name="pass" required>
         </div>
         <div>
             <label for="password" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Confirm your password</label>
             <input type="password"  id="confpass" placeholder="••••••••" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white" v-model="user.confpass" name="confpass" required >
         </div>
         </div>
         <button @click="savedUser" type="submit" class="w-full text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Create account</button>
        
     </form>
 </div>
 
 </div>
 <div v-else>
       <h4>You submitted successfully!</h4>
</div>    
 </template>
 
 <script>
 import Users from '../services/Users'
 
 export default{
     name:'add-user',
     data(){
         return {
       user: {
         id: null,
         fname: "",
         lname: "",
         email: "",
         pass: "",
         confpass: "",
         registered: true,
       },
       submitted: false
     };
   
     },
 
     methods: {
     savedUser() {
       var data = {
         fname: this.user.fname,
         lname: this.user.lname,
         email: this.user.email,
         pass: this.user.pass,
         confpass: this.user.confpass,
         registered: false,
       };
 
       Users.create(data)
         .then(response => {
           this.user.id = response.data.id;
           console.log(response.data);
           this.submitted = true;
         })
         .catch(e => {
           console.log(e);
         });
     },
     
     newUser() {
       this.submitted = false;
       this.user = {};
     }
   }
 };
 </script>