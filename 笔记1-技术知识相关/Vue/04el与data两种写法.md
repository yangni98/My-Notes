## 挂载与关联

**1 用el：‘root ’**

**2.用 v.$mount(‘root ’)**

v.  是你创建的Vue实例对象   第二种更加灵活.

```html
<div id="root">
<h1>你好 ;{{name}}</h1>

</div>
  
<script>
  const v = new Vue({
  //  el:'#root'
    
    data:{
      name:'YN'
    }
  })
 v.$mount('#root')
  console.log(v);
</script>
```



## data两种写法

1.  对象式

   ```
      data:{
         name:'YN'
       }
   ```

   

2. 函数式

```html
 data:function(){
      return{
        name:'YN'
      }
    }
```

简写开头

data(){

​	

}
