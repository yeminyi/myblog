---
layout: post
title: Getting Started Vue.js with the Simple Examples
categories: vuejs
tags: [vuejs]
---


  

## Installation

The easiest way to try out Vue.js `Direct <script> Include`, you can create an index.html file and include Vue with:

``` html

<!-- development version, includes helpful console warnings -->
<script  src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

```

or:

``` html
<!-- production version, optimized for size and speed -->
<script  src="https://cdn.jsdelivr.net/npm/vue"></script>

```
Don’t use the minified version during development. You will miss out on all the nice warnings for common mistakes.  

The other way, please refer this [link](https://vuejs.org/v2/guide/installation.html)

## Demo1

This example is using v-text,v-html,v-bind,v-on,v-cloak,v-model 

``` html
{% raw %}
<div  id="app">

<!-- {{}} text interpolation using the “Mustache” syntax (double curly braces)-->

<!-- v-text -->

<span  v-text="msg"></span>

<!-- same as -->

<span>{{msg}}</span>

  

<!-- v-cloak Hiding elements until the Vue instance is ready-->

<p  v-cloak>{{msg}} This is a message</p>

<p  v-text="msg">This is a message using v-text</p>

<!-- v-html text as html-->

<p  v-html="htmlText"  id="htmlp"></p>

<p  v-text="htmlText"  id="textp"></p>

  

<!-- v-bind Dynamically bind one or more attributes, -->
<!-- or a component prop to an expression.shorthand : -->
<!-- v-on Attaches an event listener to the element. shorthand @ -->
<input  type="button"  id="btn"  :value="buttonText"  @click="clickiMe">

<div>------:class---------------------</div>

<p  :class="['backg',flag?'fontcolor':'fontcolor1']">{{msg}}</p>

<p  :class="['backg',{'fontcolor':flag}]">{{msg}}</p>

<div>------:style---------------------</div>

<p  :style="[style1,style2]">{{msg}}</p>

<div>------v-model---two-way binding on a form input element or a component-----</div>

<input  type="text"  v-model="msg">

<button  @click="change">Change Size</button>

  

<div>------v-show and v-hide---------------------</div>

<div  v-if="isif">v-if here</div>

<div  v-show="isShow">v-show here</div>

<button  @click="hide"  id="hideBtn"  >{{btnText}}</button>

</div>
{% endraw %}
```


``` html

<script>
var vm = new Vue({
    el:"#app",
    data:{
        msg:"Hello World",
        flag:false,
        style1:{'background-color': 'brown', color:'white'},
        style2:{'font-size':"18px"},
        isif:true,
        isShow:true,
        btnText:"Hide",
        htmlText:"<b>This is HTML Text</b>",
        buttonText:"This is a button"
    },
    methods: {
        clickiMe(){
            this.buttonText="This is another button";
        },
        change(){
            if(this.style2['font-size'] == "18px")
            this.style2['font-size'] = "22px";
            else
            this.style2['font-size'] = "18px";
        },
        hide(){
            if(this.isShow==true)
            {
                this.isif=false;
                this.isShow=false;
                this.buttonText="Show";
            }
            else
            {
                this.isif=true;
                this.isShow=true;
                this.buttonText="Hide";
            }
        }
    }
})
</script>
<style>
.backg{
    background-color: aquamarine;
}
.fontcolor{
    color:red;
}
.fontcolor1{
    color:blue;
}
</style>

```
## RaffleDraw
``` html
{% raw %}
<body>
    <div id="app">
        <p>{{score}}</p>
        <p>{{level}}</p>
        <input type="button" value="Start" @click="start()" v-if ="isShow">
        <input type="button" value="Stop" @click="stop()" v-if ="!isShow">
    </div>
</body>
<script>
    var vm = new Vue({
        el: "#app",
        data: {
            score: 0,
            level: null,
            intervalIndex:null,
            isShow:true
        },
        methods: {
            start() {
                this.isShow=false;
                if(this.intervalIndex == null){
             this.intervalIndex =  setInterval(() => {
                    
                    //Math.random() 0~1
                    this.score = parseInt(Math.random() * 100);
                    //switch different prizes
                    switch (true) {
                        case this.score < 30:
                            this.level = "Participation Award"
                            break;
                        case this.score >= 30 && this.score < 65:
                            this.level = "Third Prize Winner"
                            break;
                        case this.score >= 65 && this.score < 85:
                            this.level = "Second Prize Winner"
                            break;
                        case this.score >= 85:
                            this.level = "First Prize Winner"
                            break;
                    }
                }, 50)
            }
            },
            stop(){
                this.isShow=true;
                clearInterval(this.intervalIndex);
                this.intervalIndex = null
            }
        },
    });
</script>
{% endraw %}
```
## Example of v-for 
``` html
{% raw %}
<body>
    <div id="app">
        <table>
            <tr>
                <td>No.</td>
                <td>Name</td>
                <td>Delete</td>
            </tr>
            <tr v-for="(user,index) in userList" :key="user.id" :class="{'oddStyle':isOdd(index)}">
                <td>{{user.id}}</td>
                <td v-text="user.name"></td>
                <td @click="remove(index)">Delete ---- {{index}}</td>
            </tr>
        </table>
        <input type="text" v-model="id">
        <input type="text" v-model="userName"><br>
        <button @click="addUser">Add</button>
    </div>
</body>

<script>
    var vm = new Vue({
        el: "#app",
        data: {
            userList: [
                { id: 1, name: "Alice" },
                { id: 2, name: "Bob" },
                { id: 3, name: "Jack" },
                { id: 4, name: "Tom" }
            ],
            id: 5,
            userName: ""
        },
        methods: {
            isOdd(index) {
                var res = index % 2;
                if (res == 1) return true;
                else return false;
            },
            addUser() {
                this.userList.push({ id: this.id++, name: this.userName })
            },
            remove(index){
               this.userList.splice(index,1);
            }
        },
    })
</script>
<style>
    table {
        width: 600px;
        border-collapse: collapse;
    }

    table td {
        border: 1px solid #000;
    }

    .oddStyle {
        background-color: rgb(255, 168, 168);
    }
</style>
{% endraw %}
```
## Example of v-model 
``` html
{% raw %}
<body>
    <div id="app">
        <input type="text" v-model="score">
        <br>
        <input type="range" v-model= "score" min="0" :max="maxValue">
        <br>
        <select v-model="maxValue">
            <option value="100">100</option>
            <option value="1000">1000</option>
            <option value="10000">10000</option>
        </select>
    </div>
</body>
<script>
var vm = new Vue({
    el:"#app",
    data:{
        score:50,
        maxValue:100,
    }
})
</script>
{% endraw %}
```
## Lifecycle Diagram
![Lifecycle Diagram](https://vuejs.org/images/lifecycle.png)
## Download the code
Please download the examples [here](https://github.com/yeminyi/VueSimpleDemo)
## Refer the link
Please refer the vue.js doc [here](https://vuejs.org/v2/api/)