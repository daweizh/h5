# 6. 贪吃蛇版本迭代（V6） 

- 张大为
- 辽宁师范大学计算机与信息技术学院@大连
- [https://daweizh.github.io/h5/](https://daweizh.github.io/h5/)  QQ:1243605845

## 6.1 需求说明

- 设定初始蛇身长度
- 定义蛇身容器
- 记录蛇身轨迹坐标

## 6.2 效果设计

![效果图](demo.png)

## 6.3 编程过程

1. 定义蛇长长度变量和蛇身容器变量
    ~~~js
    var snakeLength = 20;
    var pathMap = []; 
    ~~~
2. 在snakeMove方法中增加在蛇身容器中保存蛇身坐标功能
    ~~~js
    if (pathMap.length>snakeLength) {
        var snakeTail = pathMap.shift();
        game.clearRect(snakeTail['x'], snakeTail['y'], snakeUnitSize, snakeUnitSize); 
    };
    pathMap.push({'x':x,'y':y});
    ~~~
## 6.4 代码注解

~~~js
<script type="text/javascript">
    
    ....
    
    //蛇身长度
    var snakeLength = 20;
    //记录蛇运行路径
    var pathMap = []; 

    ...

    function snakeMove(){ //v3
        //v4 ...
        //保持舍身长度
        if (pathMap.length>snakeLength) {
            //删除数组第一项，并且返回该元素（蛇尾）
            var snakeTail = pathMap.shift();
            //清除蛇尾处蛇节
            game.clearRect(snakeTail['x'], snakeTail['y'], snakeUnitSize, snakeUnitSize); 
        };
        //蛇身在蛇头处增长一节
        pathMap.push({'x':x,'y':y}); 
            
        //v3 ...
    }       

    ...
</script>
~~~

## 6.5 核心代码

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
            var snakeLength = 20; //v6
            var pathMap = []; //v6

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

            function snakeMove(){ //v3
                switch(direction){ //v4 
                    case 0: //向左走
                        x = x - snakeUnitSize;
                        break; 
                    case 1: //向上走
                        y = y - snakeUnitSize;
                        break; 
                    case 2: //向右走
                        x = x + snakeUnitSize;
                        break; 
                    case 3: //向下走
                        y = y + snakeUnitSize;
                        break; 
                } 

                if(x>fieldWidth || y>fieldHeight || x<0 || y<0){ //v4
                    alert("你挂了，继续努力吧!失败原因：碰壁了....."); //v4
                    window.location.reload(); //v4
                }

                if (pathMap.length>snakeLength) { //v6
                    var snakeTail = pathMap.shift(); //v6
                    game.clearRect(snakeTail['x'], snakeTail['y'], snakeUnitSize, snakeUnitSize); //v6 
                };
                pathMap.push({'x':x,'y':y}); //v6
                
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
