# AJAX

1. 概念:  **A**synchronous **J**avascript **A**nd **X**ML 
   
   1. 异步和同步:客户端和服务器端
2. 实现方式
   1. 原生的js实现方式
   
      ```javascript
             //创建核心对象
              var xmlhttp;
              if (window.XMLHttpRequest) {// code for IE7+, Firefox, Chrome, Opera, Safari
                  xmlhttp = new XMLHttpRequest();
              } else {// code for IE6, IE5
                  xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");
              }
              //建立连接
              /**
               * 参数
               *  1.请求的方式 GET POST
               *  2.请求的url路径
               *  3.同步或异步请求 true 异步 false 同步
               */
              xmlhttp.open("GET", "ajaxServlet?name=12", true);
              //发送请求
              xmlhttp.send();
      
              //响应数据
              xmlhttp.onreadystatechange = function () {
                  if (xmlhttp.readyState == 4 && xmlhttp.status == 200) {
                      //获取服务器的响应结果
                      var text = xmlhttp.responseText;
                      alert(text);
                  }
              }
      ```
   
      
   
   2. JQuery实现方式
      1. $.ajax()
      
         ```
         $.ajax({键值对})
         ```
      
         ```javascript
           $.ajax({
                     url: "ajaxServlet",//请求路径
                     type: "POST",//请求方式
                     //data: "name = iii&...",//请求参数
                     data: {"name": "iii"},
                     success: function (date) {
                         alert(date);
                     },//响应成功后的回调函数
                 });
         ```
      
         
      
      2. $.get()
      
         ```javascript
         $.get(url,[date],[callback],[type])
         参数:
         	url:请求路径
         	date:请求参数
         	callback:回调函数
         	type:响应结果的类型
         ```
      
         ```javascript
             $.get("ajaxServlet", {name: "doudou"}, function (date) {
                 alert(date);
             });
         ```
      
         
      
      3. $.post()
      
         ```javascript
             $.post("ajaxServlet", {name: "doudou"}, function (date) {
                 alert(date);
             });
         ```

# JSON

1. 概念: JavaScript object Notation JavaScript对象表示法

2. 语法:

   1. 基本规则

      ```
      "  ":"  "
      ```

   2. 获取数据

      ```
      json对象.键名
      json对象["键名"]
      数组对象[索引]
      ```

3. JSON数据和Java对象的相互转换

   JSON解析器

   ​	常见的解析器 Jsonlib Gson fastjson jackson

   1. JSON转为Java对象

   2. Java对象转换JSON

      1. 使用步骤

         1. 导入jackson的相关jar包

         2. 创建Jackson核心对象ObjectMapper

         3. 调用相关方法进行转换

            writeValue(参数1,obj)

            writeValueAsString(obj)

      2. 注解:

         @JsonIgnoge:排除属性

         @JsonFromat:属性值得格式化

