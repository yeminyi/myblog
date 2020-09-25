---
layout: post
title: How to use Angular pipes
categories: angular
tags: [angular,pipe]
---

## Build in Pipes
- Async Pipe
- Currency Pipe
- Date Pipe
- Slice Pipe
- Decimal Pipe
- Json Pipe
- Percent Pipe
- LowerCase Pipe
- UpperCase Pipe

### Async Pipe
The Async pipe is considered the best practice when you are getting data in the form of observables. The async pipe subscribes to an Observable/Promise automatically and returns the transmitted values

``` html
    <ul>
      <li *ngFor="let users of Users | async">
        {{ users.name }}
      </li>
    </ul>
```

### The Other Pipes

``` html
{% raw %}
    <!--The content below is only a placeholder and can be replaced.--> 
    <div style = "width:100%;"> 
      <div style = "width:40%;float:left;border:solid 1px black;"> 
          <h1>Uppercase Pipe</h1> 
          <b>{{title | uppercase}}</b>
          <br/> 
          
          <h1>Lowercase Pipe</h1> 
          <b>{{title | lowercase}}</b> 
          <h1>Currency Pipe</h1> 
          <b>{{6589.23 | currency:"USD"}}</b>
          <br/> 
          
          <b>{{6589.23 | currency:"USD":true}}</b> 
          // Boolean true is used to get the sign of the currency. 
          <h1>Date pipe</h1> 
          <b>{{todaydate | date:'d/M/y'}}</b>
          <br/> 
          
          <b>{{todaydate | date:'shortTime'}}</b> 
          <h1>Decimal Pipe</h1> 
          <b>{{ 454.78787814 | number: '3.4-4' }}</b> 
          // 3 is for main integer, 4 -4 are for integers to be displayed. 
      </div> 
      
      <div style = "width:40%;float:left;border:solid 1px black;">
          <h1>Json Pipe</h1> 
          <b>{{ jsonval | json }}</b>
          <h1>Percent Pipe</h1> 
          <b>{{00.54565 | percent}}</b> 
          <h1>Slice Pipe</h1> 
          <b>{{months | slice:2:6}}</b> 
          // here 2 and 6 refers to the start and the end index 
      </div> 
    </div>
{% endraw %}
```
<b>The Other Pipes Outcome as below</b>

-----------------------------------------------------------

 Uppercase Pipe

**ANGULAR PROJECT!**  

 Lowercase Pipe

**angular project!**

 Currency Pipe

**$6,589.23**  
**$6,589.23**  // Boolean true is used to get the sign of the currency.

 Date pipe

**25/9/2020**  
**8:27 PM**

 Decimal Pipe

**454.7879**  // 3 is for main integer, 4 -4 are for integers to be displayed.

 Json Pipe

**{ "name": "Rox", "age": "25", "address": { "a1": "Mumbai", "a2": "Karnataka" } }**

 Percent Pipe

**55%**

 Slice Pipe

**Mar,April,May,Jun**  // here 2 and 6 refers to the start and the end index

-----------------------------------------

## Build a Custom Pipe

### 1. Create a Pipe
creat a pipe for truncate for example.
` ng g pipe truncate `

``` typescript

  import { Pipe, PipeTransform } from  '@angular/core';

  @Pipe({

  name:  'truncate'

  })

  export  class  TruncatePipe  implements  PipeTransform {

  transform(value: string, limit = 25, completeWords = false, ellipsis = '...') {

      if (completeWords) {

      limit = value.substr(0, limit).lastIndexOf(' ');

      }

      return  value.length > limit ? value.substr(0, limit) + ellipsis : value;

      }

  }

```
### 2. The Module Entry
   
Don't forget to add a module entry.   
If you use the angular cil, it will be added automatically.
``` typescript

@NgModule({
  declarations: [
    TruncatePipe
  ]
})
export class AppModule {}

```

### 3. Example 
   
`A really long string that needs to be truncated`
``` html
{% raw %}
      <h1>{{longStr | truncate }}</h1> 
      <!-- Outputs: A really long string that... -->

      <h1>{{longStr | truncate : 12 }}</h1> 
      <!-- Outputs: A really lon... -->

      <h1>{{longStr | truncate : 12 : true }}</h1> 
      <!-- Outputs: A really... -->

      <h1>{{longStr | truncate : 12 : false : '***' }}</h1> 
      <!-- Outputs: A really lon*** -->
{% endraw %}
```
### 4. The Other Solution to Truncate
``` html
    {% raw %}
    {{str | slice:0:6}}
    <!--  Output:      how to  -->
    If you want to append any text after slice string like
    {{ (str.length>6)? (str | slice:0:6)+'..':(str) }}
    <!--  Output:      how to...  -->
    
 {% endraw %}
```