<template>
<HeaderTop></HeaderTop>
<TabsWrapper>


  <TabMain title="Fitting"> 



<div class="row">
<div class="column">

    <select v-model="selectedCategory" @change="selectedSubcategory = ''">
      <option value="">-Main Category-</option>
      <option v-for="category in categories" :value="category.name" :key="category.name">{{ category.name }}</option>
    </select>

    <select v-if="selectedCategory" v-model="selectedSubcategory">
      <option value="">-Sub Category-</option>
      <option v-for="subcategory in getSubcategories(selectedCategory)" :value="subcategory" :key="subcategory">{{ subcategory.id }}</option>
    </select>

    <p v-if="selectedCategory || selectedSubcategory">
      You have selected {{ selectedSubcategory.id ? selectedSubcategory.id : 'all' }} from the {{ selectedCategory }} category.
    </p>
    <p v-show="selectedSubcategory!==''">
    <img class="star" :src="selectedSubcategory.img_address">
  </p>
    

</div>

<div class="column">
<span>선택 value: {{ selectedCategory }}</span><br>
<button v-show="selectedSubcategory!==''" @click="buttonClick1(selectedSubcategory.id,selectedSubcategory.f_value)">Put</button>
</div>

</div>

<div class="row">1</div>

</TabMain>


<TabMain title="Section"> 
<button @click="formLoad1">1포맷로딩(첫section,Condition)</button> <br>
<button @click="formLoad2">2Section추가</button><br>
<button @click="formLoad3">3Section삽입</button><br>
<button @click="formLoad4">4Section삭제</button><br>
<button @click="formLoad5">5Condition별write</button>
</TabMain>





<TabMain title="3_Fittings">  

<div class="row">
<div class="column">

<btn @click="myMethod('Valves1')">Valves1</btn><br>
<div v-if="type == 'Valves1'">
<button class="btnSub" v-for="item in valves1" :key="item" @click="buttonClick(item.name, item.value)">
{{ item.name }} </button>
</div>

<btn @click="myMethod('Elbows1')">Elbows</btn><br>
<div v-if="type == 'Elbows1'">
<button class="btnSub" v-for="item in elbows1" :key="item" @click="buttonClick(item.name, item.value)">
{{ item.name }} </button>
</div>

<btn @click="typeClose()">Close</btn>

</div>

<div class="column">

<span v-if="typeSub == 'ball'">
<img class="star"  src="https://ars.els-cdn.com/content/image/3-s2.0-B9781856178303000122-f12-10-9781856178303.jpg">
</span>
<span v-if="typeSub == 'butterfly'">
<img class="star" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRWN762Y9hpRVTa_QrzEyIZPbNKLLSCx_yeUA&usqp=CAU">
</span>
<span v-if="typeSub == 'check'">
<img class="star" src="data:image/png;base64,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">
</span>

<span v-if="typeSub == '90 degree'">
<img class="star"  src="https://www.fimasfitting.com/images/ff-elbow-w1.gif">
</span>
<span v-if="typeSub == '45 degree'">
<img class="star"  src="https://www.fimasfitting.com/images/ff-elbow-w2.gif">
</span>
<span v-if="typeSub == '30 degree'">
<img class="star"  src="https://www.fimasfitting.com/images/ff-elbow-w3.gif">
</span>

</div>
</div>

</TabMain>




<TabMain title="Tab 4"> 


  <h3>기능연습중</h3>
          <button @click="onSetColor">Set color</button>

  
</TabMain>




</TabsWrapper>


<FooterBottom></FooterBottom>

</template>

<script setup>
import {ref} from 'vue'

import TabsWrapper from './components/TabsWrapper.vue';
import TabMain from './components/TabMain.vue';
import HeaderTop from './components/HeaderTop.vue';
import FooterBottom from './components/FooterBottom.vue';
//import { conditionalExpression } from '@babel/types';


const valves1 = ref(
  [
  {name: 'ball', value:'ballfriction'},
{name: 'butterfly', value:'butterflyfriction'},
{name: 'Tee', value:'Teefriction'},
{name: 'check', value:'checkfriction'}])

const elbows1 = ref(
  [{name: '90 degree', value:'elbow-90'},
{name: '45 degree', value:'elbows-45'},
{name: '30 degree', value:'elbow-30'}]);

//dropdown list 
const categories = [
        {
          name: 'Valves',
          subcategories: 
          [
           {id:'Butterfly-valve' ,
          "img_address":"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRWN762Y9hpRVTa_QrzEyIZPbNKLLSCx_yeUA&usqp=CAU", 
          f_value:'1'}, 
          {id:'Ball-valve' ,
          "img_address":"https://ars.els-cdn.com/content/image/3-s2.0-B9781856178303000122-f12-10-9781856178303.jpg", 
          f_value:'2'}, 
          {id:'Check-valve' ,
          "img_address":"data:image/png;base64,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", 
          f_value:'3'}, 
          {id:'Plug-valve' ,
          "img_address":"https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhdQ9yArH5ZVn-IPVngFQcFsyPO5HsPtYNd4nQYEgx8wWtJ1Ybj_v7rv2gNCgY2Jp1qldL-h-TTc89PAGt9AMh4ZkI6QLYusScxvXD7KHS-I-TzLTUZqLo-vse3MYNi_dPwV3Af0lXRQkrOzbdmvfdKJIrEzdN8bMJ6qLLcYdhuMRGOFVqSPhg3QJIa/s705/Fluid%20Isolation%20and%20Control_2_Continued.jpg", 
          f_value:'4'}
          ]
        },
        {
          name: 'Elbows',
          subcategories: [
          {id:'Elbow(90º)' ,
          "img_address":"https://www.fimasfitting.com/images/ff-elbow-w1.gif", 
          f_value:'1'}, 
          {id:'Elbow(45º)' ,
          "img_address":"https://www.fimasfitting.com/images/ff-elbow-w2.gif", 
          f_value:'2'}, 
          {id:'Elbow(30º)' ,
          "img_address":"https://www.fimasfitting.com/images/ff-elbow-w3.gif", 
          f_value:'3'}
            
        ],
        }
      ];

      const selectedCategory = ref('');
const selectedSubcategory = ref('');


function getSubcategories(categoryName) {
    const category = categories.find((category) => category.name === categoryName);
    return category ? category.subcategories : [];
  }

    
/*이부분은 최초 변수 선언?*/
const type= ref()
const typeSub= ref()



const buttonClick = (itm1, itm2) => {
  typeSub.value = itm1;
window.Excel.run(async context => {
          const range = context.workbook.getSelectedRange();
          range.values =itm2;
          await context.sync();
        });
        alert('my message');
}

const buttonClick1 = (itm1,itm2) => {
  typeSub.value = itm1;
window.Excel.run(async context => {
          const range = context.workbook.getSelectedRange();
          range.getOffsetRange(0,0).values =itm1;
          range.getOffsetRange(0,0).format.fill.color ='yellow';
          range.getOffsetRange(1,0).values =itm2;
          range.getOffsetRange(1,0).format.fill.color ='yellow';
         
          await context.sync();
        });


}



const onSetColor= () =>{
        window.Excel.run(async context => {
          const range = context.workbook.getSelectedRange();
          range.format.fill.color = 'green';
          await context.sync();
  
        });
      }

var secNum=1

//1번폼 연습, PDC 포맷 로딩.
const formLoad1= () =>{
        window.Excel.run(async (context) => {
secNum=secNum+1
// TODO1: Queue table creation logic here.
const currentWorksheet = context.workbook.worksheets.getActiveWorksheet();
const expensesTable = currentWorksheet.tables.add("B2:E2", true /*hasHeaders*/);
expensesTable.name = "Section1";
// TODO2: Queue commands to populate the table with data.
expensesTable.getHeaderRowRange().values =
    [["Section:", secNum, "Category", "Amount"]];

expensesTable.rows.add(null /*add at the end*/, [
["","","",""],
    ["","","",""],      
    ["","","",""],
    ["F/F sum:", "=SUM(B5:E5)", "ReyNo:", "1"],

   

]);

sectionCounterTable();
// TODO3: Queue commands to format the table.
//expensesTable.columns.getItemAt(3).getRange().numberFormat = [['\u20AC#,##0.00']];
//expensesTable.getRange().format.autofitColumns();
//expensesTable.getRange().format.autofitRows();
await context.sync();
});
}

//section Counter table 추가하는 기능. 
const sectionCounterTable= () =>{
        window.Excel.run(async (context) => {
         
// TODO1: Queue table creation logic here.
const currentWorksheet = context.workbook.worksheets.getActiveWorksheet();
const expensesTable = currentWorksheet.tables.add("i2:j2", true /*hasHeaders*/);
expensesTable.name = "SectionCounter";
// TODO2: Queue commands to populate the table with data.
expensesTable.getHeaderRowRange().values =
    [["Section Counter", "."]];

expensesTable.rows.add(null /*add at the end*/, [
["Total Section","10"],
    ["Current Section","xx"],      
    ["na","na"],
    ["na", "na"],

]);
// TODO3: Queue commands to format the table.
//expensesTable.columns.getItemAt(3).getRange().numberFormat = [['\u20AC#,##0.00']];
//expensesTable.getRange().format.autofitColumns();
//expensesTable.getRange().format.autofitRows();
await context.sync();
});
}



//2번폼 연습, RANGE 입력

const formLoad2= () =>{
        window.Excel.run(async (context) => {
          let sheet = context.workbook.worksheets.getActiveWorksheet();

let range = sheet.getRange("C3:C5");
range.values = [[ 2],
[ 2],
[ 2]];
//range.format.autofitColumns();

await context.sync();
});
}


//3번폼 연습, table 내용 지우기.

const formLoad3= () =>{
        window.Excel.run(async (context) => {
          let sheet = context.workbook.worksheets.getActiveWorksheet();
    let range = sheet.getRange("A1:M100");

    range.clear();
await context.sync();
});
}

//4번폼 연습, table 내용 지우기.

const formLoad4= () =>{
        window.Excel.run(async (context) => {
          let sheet = context.workbook.worksheets.getActiveWorksheet();
    let range = sheet.getRange("A1:M100");

    range.clear();
await context.sync();
});


}
let counter=0;

const formLoad5= () =>{
console.log("1234");
counter=counter+1;

}


      function myMethod(msg) {
type.value = msg
}


function typeClose() {

type.value = false
typeSub.value = false
}




/*
   function loadSubcategories() {
      this.subcategories = this.subcategories.filter(subcategory => subcategory.categoryId === this.form.categoryId);
    }
*/



</script>



<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
  text-align: left;

}


btn {
  line-height:40px;
    width: 250px;
    text-align: center;
    padding: 10px 20px;
    margin-right: 10px;
    background-color: #ddd;
    border-radius: 14px;
    cursor: pointer;
    transition: 0.4s all ease-out;
}




btn:hover {

    width: 200px;
    text-align: center;
    padding: 10px 20px;
    margin-right: 10px;
    background-color: #4CAF50;
    border-radius: 5px;
    cursor: pointer;
    transition: 0.4s all ease-out;
}


.btnSub {
    width: 100px;
    text-align: left;
    padding: 5px 10px;
    background-color: #ffffff;
    border-radius: 3px;
    cursor: pointer;
    transition: 0.4s all ease-out;
}


.btnSub:hover {
    width: 100px;
    text-align: right;
    padding: 5px 10px;
    background-color: #c1c7c2;
    border-radius: 3px;
    cursor: pointer;
    transition: 1s all ease-out;
}



/* Form 퍼온것.*/

input[type=text], select {
  width:90%;
  padding: 5px 5px;
  margin: 4px 4px;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

input[type=submit] {
  width: 100%;
  background-color: #4CAF50;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

input[type=submit]:hover {
  background-color: #45a049;
}

div {
  border-radius: 2px;
  background-color: #f2f2f2;
  padding: 0px;
}


/* Create three equal columns that floats next to each other */
.column {
  float: left;
   width: 50%;
  min-height: 500px;

  border-radius: 2px;
  border: 0px dotted;
  outline-color:#4373a3;
  outline-style: solid;
}

/* Clear floats after the columns */
.row::after {
  content: "";
  display: table;
  clear: both;
}

img.star{
  border-radius: 2px;
  border: 2px solid #4373a3;
  width:18f0px; 
  height:152px;
  
}

</style>

