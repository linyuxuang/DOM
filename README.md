# DOM
javascript—DOM基础


            1.节点

             加载HTML页面时,Web浏览器生成一个树形结构,用来表示页面内部结构;
             DOM将这种节点结构理解为由节点组成;
             html元素为根节点;head元素是html的子节点;meta元素和title元素之间是兄弟关系;
             
             
           2.节点种类:元素节点/文本节点/属性节点
           
              <div title="元素属性">测试Div</div>
               元素节点 => div;
               属性节点 => title="元素属性"
               文本节点 => 测试Div
               
               
         元素节点查找方法
         
            方法                               说明
        getElementById()              获取特定ID元素的节点;
        getElementsByTagName()        获取相同元素的节点列表;
        getElementsByName()           获取相同名称的节点列表;
        getAttribute()                获取特定元素节点属性的值;
        setAttribute()                设置特定元素节点属性的值;
        removeAttribute()             移除特定元素节点属性;   
        
        
        1.getElementById()

         方法接收一个参数:获取元素的ID;
         如果找到相应的元素则返回该元素的HTMLDivElement对象;如果不存在,则返回null;
            document.getElementById('box');              // [object HTMLDivElement];
         当我们通过getElementById()获取到特定元素节点时,这个节点对象就被我们获取到了;
         而通过这个节点对象,我们可以访问它的一系列属性;
         
         (1).访问元素节点的属性
         
            属性                             说明
            tagName                     获取元素节点的标签名;
            innerHTML                   获取元素节点里的内容,非W3C DOM规范;
            document.getElementById('box').tagName;      // =>DIV;
            document.getElementById('box').innerHTML;    // =>测试Div;
         
         (2).访问HTML通用属性
         
            属性                             说明
            id                           元素节点的id名称;
            title                        元素节点的title属性值;
            style                        CSS内联样式属性值;
            className                    CSS元素的类;
            
            
              获取id;
            document.getElementById('box').id;   
            
               获取title;
            document.getElementById('box').title;  
            
              获取CSSStyleDeclaration对象;
            document.getElementById('box').style;  
            
              获取style对象中的color的值;也就是设置在元素行内的样式值
            document.getElementById('box').style.color;  
            
               设置style对象中的color的值;
            document.getElementById('box').style.color='red';    
            
              获取class;
            document.getElementById('box').className;  
                设置class;
            document.getElementById('box').className='pox';     

            document.getElementById('box').bbb;          // 获取自定义属性的值,非IE不支持;
         
         
         
         
     2.getElementsByTagName()
     
           方法返回一个对象数组HTMLCollection(NodeList)数组,这个数组保存着所有相同元素名的节点列表;
          document.getElementsByTagName('*');         // 利用通配符获取所有元素;
          // PS:IE在使用通配符时,会把文档最开始的html的规范声明当作第一个元素节点;

          document.getElementsByTagName('li');        // =>[object HTMLCollection];获取所有li元素;
          document.getElementsByTagName('li').[0];    // 获取第一个li元素;
    
    
    
    3.getElementsByName()

       获取相同名称(name)设置的元素,返回一个对象数组HTMLCollection(NodeList);
         document.getElementsByName('add');          // 获取具有name='add'的input元素集合;
           // PS:对于并不是HTML合法的属性,那么在JS获取的兼容性上也会存在差异;
           // IE支持合法的name属性,但对于自定义的属性会出现不兼容问题;
    
    
   4.getAttribute()
   
     方法将获取元素中某个属性值;
     但它和直接使用".attr"获取属性值的方法有一定区别;
         document.getElementById('box').getAttribute('mydiv');    // 获取自定义属性值;
         document.getElementById('box').mydiv;                    // 获取自定义属性值,仅IE支持; 
    
    
    
    5.setAttribute()
    
       方法将设置元素中某个属性和值;接收两个参数:属性名和值;
       如果属性本身已存在,那么就会覆盖;
       
       
        设置属性和值    //;<div id="box" align="center"> 
           document.getElementById('box').setAttribute('align','center');   
           // PS:在IE7及以下,使用setAttribute()方法设置class和style属性没有效果;
    
    
    6.removeAttribute()
      方法可以移除HTML属性;
      document.getElementById('box').removeAttribute('style');  // 移除style样式属性;
    
    
    
    DOM节点

            1.node节点属性

            节点可以分为:元素节点/属性节点和文本节点;
            这些节点都有三个属性:nodeName/nodeType和nodeValue;

                              信息节点属性
             节点类型            nodeName            nodeType         nodeValue 
               元素                 元素名称             1              null
               属性                 属性名称             2              属性值 
               文本                 #text               3              文本内容
               
               document.getElementById('box').nodeType;            // =>1; 元素节点;
    
    层次节点属性
    
    
                    属性                         说明 
                childNodes             读取当前元素节点的所有子节点;
                
                firstChild             读取当前元素节点的第一个子节点;
                
                lastChild              获取当前元素节点的最后一个子节点;
                
                ownerDocument          获取该节点的文档根节点,相当于document;
                
                hasChildNodes           检查元素是否有子节点：(有子节点返回true，没有返回 false)
                
                parentNode             获取当前节点的父节点;
                
                previousSibling        获取当前节点的前一个同级节点;
                
                nextSibling            获取当前节点的后一个同级节点;
                
                attributes             获取当前元素节点的所有属性节点集合;
    
    
    
    
    (1).childNodes属性
    
               属性获取某一个元素节点的所有子节点,这些子节点包含元素节点和文本节点;
               
               PS:使用childNodes[n]返回子节点对象的时候,
               有可能返回的是元素子节点,比如:HTMLElement;
               也可能返回的是文本子节点,比如:Text;
               元素子节点可以使用nodeName或者tagName获取标签名称;
               而文本子节点可以使用nodeValue获取;
                  var box = document.getElementById('box');
                  for(var i=0; i<box.childNodes.length; i++){
                       判断是元素节点,输出元素标签名;
                      if(box.childNodes[i].nodeType === 1){
                          console.log('元素节点:'+box.childNodes[i].nodeName);
                       判断是文本节点,输出文本内容;
                      }else if(box.childNodes[i].nodeType ===3){
                          console.log('文本节点:'+box.childNodes[i].nodeValue);
                      }
                  }
                   PS1:在获取到文本节点(重点在于已经不是元素节点)的时候,
                   是无法使用innerHTML这个属性输出文本内容的;
                   这个非标准的属性必须在获取元素节点的时候,
                   才能输出里面包含的文本;
                      alert(box.innerHTML);     innerHTML和nodeValue第一个区别;

                   PS2:innerHTML和nodeValue在赋值的时候,
                   nodeValue会把包含在文本里的HTML转义成特殊的字符,
                   从而达到形成纯文本的效果;

                   而innerHTML会解析文本里的特殊字符;
                      box.childNodes[0].nodeValue = '<strong>abc</strong>';  =><strong>abc</strong>;
                      box.innerHTML = '<strong>abc</strong>';       =>abc(样式加粗);
    
    
    
  (2).firstChild和lastChild属性

             firstChild 等价于 childNodes[0];获取当前元素的第一个子节点;
             lastChild  等价于 childNodes[box.childNodes.length-1];获取当前元素最后一个子节点;  
    
    
   (4).parentNode/previousSibling/nextSibling属性

             parentNode:返回该节点的父节点;
             previousSibling:返回该节点的前一个同级节点;
             nextSibling:返回该节点的后一个同级节点;
              alert(box.parentNode.nodeName);                      // 获取父节点的标签名;
              alert(box.firstChild.nextSibling);                   // 获取第二个节点;
              alert(box.lastChild.previousSibling);                // 获取倒数第二个节点; 
        
        
        
     四 节点操作
         DOM不单单可以查找节点,也可以创建节点/复制节点/插入节点/删除节点和替换节点

                  节点操作方法
                  
                      方法                     说明 
                  write()             这个方法可以把任意字符串插入到文档中;
                  
                  createElement()     创建一个元素节点;
                  
                  appendChild()       将新节点追加到子节点列表的末尾;
                  
                  createTextNode()    创建一个文件节点;
                  
                  insertBefore()      可以把节点添加到指定节点的前面(前后都可以
                  
                  replaceChild()      方法可将某个子节点替换为另一个
                  
                  cloneNode()         复制节点;
                  
                  removeChild()       移除节点;   
                  
                  normalize()        合并相邻的 Text 节点并删除空的 Text 节点。
         
        (1).write()方法
            // write()方法可以把任意字符串插入到文档中去;
            document.write('<p>这是一个段落!</p>'); // 解析后文字;   
        
        (2).createElement()方法
                createElement()方法可以创建一个元素节点;
                    var box= document.getElementById("box");
                        var text= document.createElement('p');
                       box.appendChild(text)  
                                   
        
         (3).appendChild()方法
              appendChild()方法将一个新节点添加到某个节点的子节点列表的末尾上;
              var box = document.getElementById('box'); 
              var p = document.createElement('p'); // 创建一个新元素节点<p>;
              box.appendChild(p); // 把新元素节点<p>添加子节点末尾; 
        
                 
                   
            (4).createTextNode()方法
                该方法创建一个文本节点;
                var text = document.createTextNode('段落'); 
                p.appendChild(text); // 将文本节点添加到子节点末尾;  
        
        
            (5).insertBefore()方法
                      该方法可以把节点添加到指定节点的前面(前后都可以);
                      
                    function myFunction()
                      {
                      var newItem=document.createElement("LI")
                      var textnode=document.createTextNode("Water")
                      newItem.appendChild(textnode)

                      var list=document.getElementById("myList")
                          list.insertBefore(newItem,list.childNodes[0]);
                        }   
                        
                        输出    <ul id="myList"> 
                                 <li>Water</li>
                                 <li>Tea</li>
                                 </ul>
                                 
           
          (6) replaceChild() 方法可将某个子节点替换为另一个。

                   如替换成功，此方法可返回被替换的节点，如替换失败，则返回 NULL。。
                   
           
                        <ul id="myList"><li>Coffee</li><li>Tea</li><li>Milk</li></ul>
                        <button onclick="myFunction()">试一下</button>

                        function myFunction()
                          {
                             创建新文本
                         var textnode=document.createTextNode("Water");
                                  // 找到第一个 li 
                         var item=document.getElementById("myList").childNodes[0]; 
                               把以前li的第一个子节点文本替换成 新创建的文本
                         item.replaceChild(textnode,item.childNodes[0]);
                
                         }    
                         
                         

        (7).cloneNode()方法

          // 该方法可以把子节点复制出来;复制后返回的节点副本属于文档所有,但并没有为它指定父节点;
          // 参数为true:执行深复制,就是复制节点及其整个子节点树;
          // 参数为false:执行浅复制,只复制节点本身;
              var box = document.getElementById('box');
              var clone = box.firstChild.cloneNode(true); // 获取第一个子节点,true表示复制内容;
              box.appendChild(clone);   // 添加到子节点列表末尾;
             
               输出     <div id="box">
                          <p>第一个子节点</p>
                          <a>第二个子节点</a>
                           <p>第一个子节点</p>
                        </div>   
                        
              var box = document.getElementById('box');
              var clone = box.firstChild.cloneNode(false); //false:执行浅复制,只复制节点本身;;
              box.appendChild(clone);  

               输出    <div id="box">
                          <p>第一个子节点</p>
                          <a>第二个子节点</a>
                           <p></p>
                        </div> 
                        
                        
            (8).removeChild()方法
                  该方法删除指定节点;
                      
                      下面两种方式是等价的
                   var box = document.getElementById('box');

                     删除在body里面的box元素删除
                     document.body.removeChild(box);  

                     删除在box父元素里面的box元素删除 (box的父元素就是body)
                     box.parentNode.removeChild(box)     
                        

             (9)  normalize()    合并相邻的 Text 节点并删除空的 Text 节点。
                
                        <p id="demo">点击添加按钮，给该p元素添加文本，点击正规化按钮使该p元素正规化</p>

                        <button onclick="addTextNode()">添加</button>

                        <button onclick="normPara()">正规化</button>

                        <p>以上文本中有<span id="myS">1</span>个子节点</p>

                        <p id="demo"></p>   

                        function addTextNode() {

                            var x = document.createTextNode("添加了文本.");

                            var y = document.getElementById("demo");

                            y.appendChild(x);

                            var x = document.getElementById("myS");

                            x.innerHTML = y.childNodes.length;

                        }

                        function normPara() {

                            var x = document.getElementById("demo");  

                            x.normalize();

                            var y = document.getElementById("myS");

                            y.innerHTML = x.childNodes.length;


                        }


  取得特性

              getAttribute() 
  
                        <div id="myDiv" class="myClass" title="myTitle"></div>

                          var div=document.getElementById("myDiv");
                          console.log(div.getAttribute("id"))   myDiv
                          console.log(div.getAttribute("class"))  myClass
                          console.log(div.getAttribute("title"))  myTitle

设置特性
             
                 setAttribute(n1,n2)
             
                       var div=document.getElementById("myDiv");
                         console.log(div.setAttribute("id","myid")) 
                         console.log(div.getAttribute("class","myclass"))
                         console.log(div.getAttribute("title","mytitle"))

删除特性  
        
            removeAttribute（）
                     
                   div.removeAttribute("id")

