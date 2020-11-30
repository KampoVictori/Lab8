<template>
<div class="bookkeeping"> 
  <input type="button" value="Додати" v-on:click="showForm" >
  <input type="button" value="Редагувати" v-on:click="showEditForm" >
  <input type="button" value="Видалити" v-on:click="deleteWorker" >
  <input type="button" value="Знайти" v-on:click="showfindWorker" >
  <div class="wrap"> 
  <form  v-on:submit.prevent = "addNewWorker" class="newForm" v-if="showNewWorkerForm">
    ПІБ <input type="text" v-model="newWorker.nameW"><br>
    Посада <input type="text" v-model="newWorker.post"> <br>
    З/п <input type="number" v-model.number="newWorker.salary"> <br>
    К-сть дітей <input type="number" v-model.number="newWorker.count_child" > <br>
    Стаж <input type="number" v-model.number="newWorker.experience" > <br>
    <button type="submit" >Додати </button>
    <button type="reset"> Очистити </button>
  </form>
  </div>
<ul>
    <li v-for="(b, i) in worker" :key="i" class="bookkeeping" v-on:click="selectWorker(i)" :style="i==selected?'box-shadow: 0 0 20px rgba(0,0,0,0.5);':'' ">
      <h3>ПІБ: {{ b.nameW }}</h3>
      <h3>Посада: {{ b.post }}</h3>
      <h3>З/п: {{ b.salary }}</h3>
      <h3>К-сть дітей: {{ b.count_child }}</h3>
      <h3>Стаж: {{ b.experience }}</h3>
    </li>
  </ul>
  <form  v-on:submit.prevent = "editSelectedWorker" class="newForm" v-if="showEditWorkerForm">
    ПІБ <input v-model="editWorker.nameW"><br>
    Посада <input v-model="editWorker.post"> <br>
    З/п <input type="number" v-model.number="editWorker.salary"> <br>
    К-сть дітей <input type="number" v-model.number="editWorker.count_child" > <br>
    Стаж <input type="number" v-model.number="editWorker.experience" > <br>
    <button type="submit" >Редагувати </button>
    <button type="reset"> Очистити </button>
  </form>
  <form  v-on:submit.prevent = "Findworker" class="newForm" v-if="showFindWorkerForm">
    Посада <input type="text" v-model="workerPost"> <br>
    К-сть дітей <input type="number" v-model.number="children_count" > <br>
    <button type="submit" >Знайти </button>
    <button type="reset"> Очистити </button>
  </form>
</div>
</template>

<script>
export default{
    name:"App", 
    data(){
      return {
      selected:-1,
      showNewWorkerForm: false,
      showEditWorkerForm: false,
      showFindWorkerForm: false,
      workerPost: "",
      children_count:0,
        worker:[{
          nameW: "Ліда",
          post:"Прибиральниця",
          salary: 7000,
          count_child: 3,
          experience: 10
        },
        {
          nameW: "Джон",
          post:"Адміністратор",
          salary: 10500,
          count_child: 2,
          experience: 4
        },
        {
          nameW: "Едвард",
          post:"Охоронець",
          salary: 8000,
          count_child: 5,
          experience: 2
        }],
        newWorker: {
          nameW: "",
          post:"",
          salary: 0,
          count_child: 0,
          experience: 0       
        },
        editWorker:null,
      };
    },
    methods: {
    addNewWorker(){
      let newWorkerCopy = Object.assign({}, this.newWorker)
      this.worker.push(newWorkerCopy)
      this.showNewWorkerForm = false
    },
    showForm(){
       this.showNewWorkerForm =true;
    },
    selectWorker(index){
      this.selected = index;
    },
    showEditForm(){
      if (this.selected>=0){
         this.editWorker = this.worker[this.selected];
        this.showEditWorkerForm = true;
      }
      else alert("Виберіть працівника")
    },
    editSelectedWorker(){
      this.showEditWorkerForm = false;
    },
    showfindWorker(){
      this.showFindWorkerForm=true;
    },
    Findworker(){
      var p=this.workerPost;
      var z=this.children_count;
      this.worker=this.worker.filter(x=>x.post==p && x.count_child<=z);
      this.showFindWorkerForm=false;
    },
    deleteWorker(){
      if (this.selected>=0)
        this.worker.splice(this.selected, 1);
    }
  },
};
</script>
<style>
body{
  background:url(https://i1.wp.com/hipzmag.com/wp-content/uploads/2018/12/novogodnij-fon-2018.jpg);
  background-size: 100%;
  text-align: center;
}
ul{
  list-style: none;
}
.bookkeeping {
  padding: 50px;
  padding-top: 0px;
}
.newForm{
  text-align: left;
  display: inline-block;
   font:14px Arial, Helvetica, sans-serif;
   margin-top: 20px;
}
input{
  background: linear-gradient(0deg, rgba(255,255,255,0.9026961126247374) 0%, rgba(176,175,174,1) 100%);
}
input[type=button]{
text-align:center; 
 padding:11px 33px;   
 font:18px Arial, Helvetica, sans-serif; 
 font-weight:bold; 
 box-shadow:1px 1px 5px #000000, inset 0px 0px 1px #ffffff;  
 text-shadow: 2px 1px 0px #adabab; 
 }

 input[type=button]:hover{
 padding:15px 40px; 
 font:18px Arial, Helvetica, sans-serif; 
 font-weight:bold; 
 color:#000000; 
 box-shadow:3px 3px 6px #000000, inset 0px 0px 1px #ffffff;  
 text-shadow: 2px 1px 0px #adabab; 
}
li{
    background: linear-gradient(0deg, rgba(255,255,255,0.9026961126247374) 0%, rgba(176,175,174,1) 100%);
    margin: 20px;
    width: 130px;
    display: inline-block;
}
</style>
