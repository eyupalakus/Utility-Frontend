<template>
  <div class="border-2 w-3/4 m-auto h-full rounded-md bg-white 	">
    <div class="text-3xl pt-20 text-center">
      <h1>Utility</h1>
    </div>
    <div class="mr-auto ">              
        <form @submit.prevent="Create()" class="w-full  bg-white text-left pl-20 rounded-xl pt-20 ">
            
            <label  class="text-gray-800 inline-block text-xs uppercase tracking-wider font-bold mt-4 mb-8 mx-0">MS OFFICE :</label>
            <input v-model="put.msoffice" class="ml-4 w-1/5 box-border px-6 py-3 border-solid border-black border-2 " type="text" required >

            <label class="ml-4 text-gray-800 inline-block text-xs uppercase tracking-wider font-bold mt-4 mb-8 mx-0">PROGRAMING LANGUAGE :</label>
            <input v-model="put.programing" class="ml-4 w-1/5 box-border px-6 py-3 border-solid border-black border-2" type="text" required >

            <label class="ml-4 text-gray-800 inline-block text-xs uppercase tracking-wider font-bold mt-4 mb-8 mx-0">LANGUAGE :</label>
            <input v-model="put.languages" class="ml-4 w-1/5 box-border px-6 py-3 border-solid border-black border-2 " type="tel" required>
            <button type="submit" class="rounded-full border-2 h-10 ml-72 bg-gradient-to-r from-pink-500 hover:to-yellow-500 hover:from-green-400 to-blue-500 text-neutral-50 mt-10 w-1/2" >Save</button>

        </form>                   
    </div>    
    <div class=" h-screen w-4/5 m-auto pt-20 ">
      <table class="table-auto justify-end w-full text-center ">
        <thead class="bg-gray-600 w-full text-slate-100">
          <tr >
            <th class="py-4" >ID</th>
            <th >MS OFFICE</th>
            <th >PROGRAMING LANGUAGE</th>
            <th>LANGUAGE</th>
            <th>ACTION</th>
          </tr>
        </thead>        
        <tbody class="border-t-2 text-slate-900">          
          <tr v-for="ut in utility" :key="ut.Id">
            <td>{{ ut.id }}</td>
            <td >{{ ut.msoffice }}</td>
            <td >{{ ut.programing }}</td>
            <td >{{ ut.languages }}</td>
            <td>
              <button class=" border-1 h-10  bg-blue-500 text-neutral-50 mt-2 w-1/2" @click="Edit(ut.id)">Edit</button>
              <button class=" border-1 h-10  bg-red-500 text-neutral-50 mt-2 w-1/2" @click="Delete(ut.id)">Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
  
</template>

<script>

import axios from'axios'


export default {
  name: 'App',

  
  data(){
    return{
      id:false,
      post:{
        msoffice:'',
        programing:'',
        languages:''
      },
      put:{
        id:'',
        msoffice:'',
        programing:'',
        languages:''
      },
      utility:null,
    };
  },
  created:function(){
    axios.get("http://localhost:5243/api/Utility").then(res=>{
      this.utility=res.data
      console.log(this.utility)
    });
  },
  methods:{    
    Create(){
      this.post.msoffice=this.put.msoffice
      this.post.programing=this.put.programing
      this.post.languages=this.put.languages
      if(this.id==false){
        axios.post("http://localhost:5243/api/Utility",this.post
        )
      }
      else{
        axios.put("http://localhost:5243/api/Utility",{
          id:this.put.id,
          msoffice:this.put.msoffice,
          programing:this.put.programing,
          languages:this.put.languages
        })
      }
      
    },
    Edit(ut){
      axios.get("http://localhost:5243/api/Utility"+"/"+ut).then(res=>{
      this.id=true,
      this.put.id=res.data.id
      this.put.msoffice=res.data.msoffice
      this.put.programing=res.data.programing
      this.put.languages=res.data.languages
      console.log(res.data.id)
    })
//  axios.push("http://localhost:5243/api/Utility",{
   //   id:this.id,
    //  msoffice:this.post.msoffice,
     // programing:
  //  })
    },
    Delete(ut){
      axios.delete("http://localhost:5243/api/Utility"+"/"+ut,ut
      )
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  height: screen;background: linear-gradient(90deg, bisque, lightsalmon);
}
</style>
