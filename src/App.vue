<template>
<HeaderTop></HeaderTop>
<TabsWrapper>
<TabMain title="Tab 1"> 

  <div class="row">
  <div class="column">

  <btn @click="myMethod('Valves')">Valves</btn><br>
  <div v-if="type == 'Valves'">
  <button v-for="item in valves" :key="item" @click="buttonClick(item.name)">
{{ item.name }} / {{ item.value }}</button>
</div>

<btn @click="myMethod('Elbows')">Elbows</btn><br>
  <div v-if="type == 'Elbows'">
  <button v-for="item in elbows" :key="item" @click="buttonClick(item.name)">
{{ item.name }} / {{ item.value }}</button>
</div>

</div>

<div class="column">

<btn @click="myMethod('Valves')">Valves</btn><br>
<div v-if="type == 'Valves'">
<button v-for="item in valves" :key="item" @click="buttonClick(item.name)">
{{ item.name }} / {{ item.value }}</button>
</div>

<btn @click="myMethod('Elbows')">Elbows</btn><br>
<div v-if="type == 'Elbows'">
<button v-for="item in elbows" :key="item" @click="buttonClick(item.name)">
{{ item.name }} / {{ item.value }}</button>
</div>

</div>
</div>

</TabMain>




<TabMain title="Tab 2"> 

  <div class="dropdown">
  <button  @click="myMethod('ball')">Valves</button>
  <div class="dropdownContent">
    <div v-if="type == 'Valves'">
  <button v-for="item in valves" :key="item" @click="buttonClick(item.name)">
{{ item.name }} / {{ item.value }}</button>
</div>



  <a  @click="myMethod('ball')">Ball</a>
  <a @click="myMethod('butterfly')">Butterfly</a>
  <a @click="myMethod('check')">Check</a>
  </div>
</div>
<div v-if="type == 'ball'">
  <button v-for="item in data1" :key="item" @click="buttonClick(item.name)">
{{ item.name }} / {{ item.value }}</button>
</div>
<div v-if="type == 'butterfly'">
  <img src="data:image/jpeg;base64,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" alt="">
</div>

<br>

<div class="dropdown">
  <button class="dropbtn">Elbow</button>
  <div class="dropdownContent">
  <a href="#">90 Degree</a>
  <a href="#">45 Degree</a>
  <a href="#">User Define</a>
  </div>
</div>

<br>



</TabMain>




<TabMain title="Tab 3"> 
  
  <div>
  <form action="/action_page.php">
    <label for="country">Country</label>
    <select id="country" name="country">
      <option value="australia" @click="buttonClick2('australia')">Australia</option>
      <option value="canada">Canada</option>
      <option value="usa">USA</option>
    </select>
  
    <input type="submit" value="Submit">
  </form>
</div>

<div>
  <form action="/action_page.php">
    <select id="countr" name="countr">
      <option v-for="item in data2" :key="item" @click="buttonClick(item.name)">
        {{ item.name }} / {{ item.value }}
      </option>
      
    </select>
  
    <input type="submit" value="Submit" @click="buttonClick(item.name)">
  </form>
</div>


</TabMain>




<TabMain title="Tab 6"> Hello from Tab4 </TabMain>




</TabsWrapper>


<FooterBottom></FooterBottom>

</template>

<script setup>
import {ref} from 'vue'

import TabsWrapper from './components/TabsWrapper.vue';
import TabMain from './components/TabMain.vue';
import HeaderTop from './components/HeaderTop.vue';
import FooterBottom from './components/FooterBottom.vue';

function myMethod(msg) {

type.value = msg
}

const valves = ref(
  [{name: 'ball', value:23},
{name: 'butterfly', value:23},
{name: 'check', value:23}])

const elbows = ref(
  [{name: '90 degree', value:23},
{name: '45 degree', value:23},
{name: '30 degree', value:23}])

const data1 = ref(
  [{name: 'valve', value:23},
{name: 'Tee', value:23},
{name: 'Elbow', value:23}])

const data2 = ref(
  [{name: 'pump1', value:23},
{name: 'pump2', value:23},
{name: 'pump3', value:23}])


/*이부분은 이해안됨, type ref 가뭔가*/
const type= ref()


const buttonClick = (value) => {
  
  if(value == 'pump1'){
    alert('1번 펌프를 선택하셨습니다. 다음단계로 넘어가주세요')
  } else if( value == 'pump2'){
    alert("왜 선택하셨어요... 님 도른")
  } else {
    alert ('2')
  }
}

const buttonClick2 = () => {

    alert ('2')
  
}

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
  line-height:40px;
}


btn {
    width: 200px;
    text-align: center;
    padding: 10px 20px;
    margin-right: 10px;
    background-color: #ddd;
    border-radius: 5px;
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




  /* Style The Dropdown Button */
.dropbtn {
  background-color: #7cba90;
  color: white;
  padding: 10px;
  font-size: 16px;
  border: none;
  cursor: pointer;
  width: 150px;
  border-radius: 5px;
}

/* The container <div> - needed to position the dropdown content */
.dropdown {
  position: relative;
  display: inline-block;
}

/* Dropdown Content (Hidden by Default) */
.dropdownContent {
  display: none;
  position: absolute;
  background-color: #f9f9f9;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
  z-index: 1;
}

/* Links inside the dropdown */
.dropdownContent a {
  color: black;
  padding: 6px 8px;
  text-decoration: none;
  display: block;
}

/* Change color of dropdown links on hover */
.dropdownContent a:hover {background-color: #f1f1f1}

/* Show the dropdown menu on hover */
.dropdown:hover .dropdownContent {
  display: block;
}

/* Change the background color of the dropdown button when the dropdown content is shown */
.dropdown:hover .dropbtn {
  background-color: #3e8e41;
}


/* Form 퍼온것.*/

input[type=text], select {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
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
  border-radius: 5px;
  background-color: #f2f2f2;
  padding: 20px;
}

/* Create three equal columns that floats next to each other */
.column {
  float: left;
  width: 33.33%;
  padding: 15px;
}

/* Clear floats after the columns */
.row::after {
  content: "";
  display: table;
  clear: both;
}


</style>
