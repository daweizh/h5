# 5. 贪吃蛇版本迭代（V5） 

- 张大为
- 辽宁师范大学计算机与信息技术学院@大连
- [https://daweizh.github.io/h5/](https://daweizh.github.io/h5/)  QQ:1243605845

## 5.1 需求说明

- 读取按键码，并转换成0~3四个方向值

## 5.2 效果设计

![效果图](demo.png)

## 5.3 编程过程

- 增加按键事件处理函数
    ~~~js
    document.onkeydown = function(e) {
        var code = e.keyCode - 37; 
        switch(code){ 
            case 0 : //按向左键
                direction = 0;
                break; 
            case 1 : //按向上键
                direction = 1;
                break; 
            case 2 : //按向右键
                direction = 2;
                break; 
            case 3 : //按向下键
                direction = 3;
                break; 
        } 
    } 
    ~~~

## 5.4 代码注解

~~~js
<script type="text/javascript">
    //v1 ... v4
    /*
     * 接收键盘按键事件处理功能，用来改变蛇的前进方向。
     */
    document.onkeydown = function(e) {
        //读取按键码，并转换成0~3四个方向值
        var code = e.keyCode - 37; 
        switch(code){ 
            case 0 : //按向左键
                direction = 0;
                break; 
            case 1 : //按向上键
                direction = 1;
                break; 
            case 2 : //按向右键
                direction = 2;
                break; 
            case 3 : //按向下键
                direction = 3;
                break; 
        } 
    } 
</script>
~~~

## 5.5 核心代码

~~~
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Greedy Snake</title>
        <style type="text/css">
            div { /*v1*/
                width:400px;
                margin:0 auto;  
            }
            canvas { /*v1*/
                background:#abcdef;
                border:1px solid #000000;
            }
        </style>
        <script type="text/javascript">
            var field; //v1
            var game; //v1
            var fieldWidth; //v2
            var fieldHeight; //v2
            var speed = 160; //v2
            var foodX = foodY = 0; //v2
            var snakeUnitSize = 8; //v2
            var x = y = snakeUnitSize; //v3
            var direction = 3; //v4

            window.onload = function(){ //v1
                field = document.getElementById("field"); //v1
                game = field.getContext("2d"); //v1
                fieldWidth = field.width; //v2
                fieldHeight = field.height; //v2
                window.setInterval(snakeMove, speed); //v3
            }

            document.onkeydown = function(e) { //v5
                var code = e.keyCode - 37; //v5
                switch(code){ //v5
                    case 0 : //按向左键
                        direction = 0;  //v5
                        break; 
                    case 1 : //按向上键
                        direction = 1; //v5
                        break; 
                    case 2 : //按向右键
                        direction = 2;  //v5
                        break; 
                    case 3 : //按向下键
                        direction = 3;  //v5
                        break; 
                } 
            } 

            function snakeMove(){ //v3
                switch(direction){ //v4 
                    case 0: //向左走
                        x = x - snakeUnitSize; //v4
                        break; 
                    case 1: //向上走
                        y = y - snakeUnitSize; //v4
                        break; 
                    case 2: //向右走
                        x = x + snakeUnitSize; //v4
                        break; 
                    case 3: //向下走
                        y = y + snakeUnitSize; //v4
                        break; 
                } 

                if(x>fieldWidth || y>fieldHeight || x<0 || y<0){ //v4
                    alert("你挂了，继续努力吧!失败原因：碰壁了....."); //v4
                    window.location.reload(); //v4
                }
                
                game.fillStyle = "#006699"; //v3
                game.strokeStyle = "#006699"; //v3
                game.fillRect(x, y, snakeUnitSize, snakeUnitSize); //v3
            }       

            function putFood(){ //v2
                var size = snakeUnitSize; //v2
                game.fillStyle = "#ff0000"; //v2
                game.strokeStyle = "#000000"; //v2
                foodX = Math.ceil(Math.random() * (fieldWidth/size)); //v2
                foodY = Math.ceil(Math.random() * (fieldHeight/size)); //v2
                game.fillRect(foodX*size, foodY*size, size, size); //v2
            } 
        </script>
    </head>
    <body>
        <!-- v1 -->
        <h2 align="center">Greedy Snake</h2>
        <!-- v1 -->
        <div>
            <!-- v1 -->
            <canvas id="field" width="400" height="600">
                This is the field that snake snaking.
            </canvas>
        </div>
    </body>
</html>
~~~

## w.微信订阅号

1. 智数精英-关注中小学程序设计及相关讨论
2. 随话录-记录小朋友们的成长时光
2. 西山征途-关注大学生成长、学习和生活

![欢迎关注“智数精英”订阅号](../../assets/me/img/idea8.jpg)
![欢迎关注“随话录”订阅号](../../assets/me/img/shl8.jpg)
![欢迎关注“西山征途”订阅号](../../assets/me/img/xszt8.jpg)

----------

## b.[返回](../)

## h.[首页](../../)
