# 9. 贪吃蛇版本迭代（V9） 

- 张大为
- 辽宁师范大学计算机与信息技术学院@大连
- [https://daweizh.github.io/h5/](https://daweizh.github.io/h5/)  QQ:1243605845

## 9.1 需求说明

- 重构网页布局增加游戏状态显示
- 增加游戏状态记录变量
- 增加消息栏对象变量
- 增加游戏状态收集功能
- 增加游戏状态显示功能

## 9.2 效果设计

![效果图](demo.png)

## 9.3 编程过程

1. 重构网页布局，将`<body>`标记内容替换成如下内容
    ~~~html
    <center>
        <h2>Greedy Snake</h2>
        <table>
            <tr>
                <td>
                    <canvas id="field" width="400" height="600">
                        This is the field that snake snaking.
                    </canvas>
                </td>
                <td valign="top" align="left">
                    <table class="show">
                        <tr>
                            <td align="right">贪吃蛇长度：</td>
                            <td align="left" id="snakes">35</td>
                        </tr>
                        <tr>
                            <td align="right">捕食数量：</td>
                            <td align="left" id="foods">14</td>
                        </tr>
                        <tr>
                            <td align="right">行走步数：</td>
                            <td align="left" id="steps">1000</td>
                        </tr>
                        <tr>
                            <td align="right">食物位置：</td>
                            <td align="left" id="foodPlace">14</td>
                        </tr>
                        <tr>
                            <td align="right">蛇头位置：</td>
                            <td align="left" id="snakePlace">1000</td>
                        </tr>
                    </table>
                </td>
            </tr>
        </table>
    </center>
    ~~~
2. 删除`div`样式，增加`.show`样式
    ~~~css
    .show{
        font-family: "微软雅黑";
        font-size: large;
        font-weight: bold;
    }
    ~~~
3. 增加游戏状态计数变量
    ~~~js
    var foodNumber = -1;
    var walkSteps = 0;
    ~~~
4. 增加游戏状态消息栏变量
    ~~~js
    var foods;
    var snakes;
    var foodPlace;
    var snakePlace;
    var steps;
    ~~~
5. 在`widnow.onload`方法中获取状态栏对象
    ~~~js
    foods = document.getElementById("foods");
    snakes = document.getElementById("snakes");
    steps = document.getElementById("steps");
    foodPlace = document.getElementById("foodPlace");
    snakePlace = document.getElementById("snakePlace");
    ~~~
6. 在`snakeMove`方法中搜集游戏状态信息，显示游戏状态
    ~~~js
    walkSteps = walkSteps + 1;
    dispMessage();
    ~~~
7. 在 `putFood`方法中搜集游戏状态信息
    ~~~js
    foodNumber = foodNumber + 1;
    walkSteps = 0;
    ~~~
8. 增加游戏状态刷新方法
    ~~~js
    function dispMessage(){
        foods.innerHTML = foodNumber;
        snakes.innerHTML = snakeLength;
        steps.innerHTML = walkSteps;
        foodPlace.innerHTML = "(" + foodX*snakeUnitSize + "," + foodY*snakeUnitSize + ")";
        snakePlace.innerHTML = "(" + x + "," + y + ")";
    }
    ~~~        
    
## 9.4 代码注解

~~~
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Greedy Snake</title>
        <style type="text/css">
            ... ...
            /*消息板样式*/
            .show{ /*v9*/
                font-family: "微软雅黑";
                font-size: large;
                font-weight: bold;
            }
        </style>
        <script type="text/javascript">
            ... ...
            //吃到食物的数量
            var foodNumber = -1; //v9
            //蛇走了多少步
            var walkSteps = 0; //v9
            //捕食数量消息栏
            var foods; //v9
            //蛇长消息栏
            var snakes; //v9
            //食物位置消息栏
            var foodPlace; //v9
            //蛇头位置消息栏
            var snakePlace; //v9
            //蛇行步数消息栏
            var steps; //v9
            
            window.onload = function(){ //v1
                //获取捕食数量消息栏
                foods = document.getElementById("foods"); //v9
                //获取蛇长消息栏
                snakes = document.getElementById("snakes"); //v9
                //获取蛇行步数消息栏
                steps = document.getElementById("steps"); //v9
                //获取食物位置消息栏
                foodPlace = document.getElementById("foodPlace"); //v9
                //获取蛇头位置消息栏
                snakePlace = document.getElementById("snakePlace"); //v9

                ... ...
            }

            ... ...

            function snakeMove(){ //v3
                ... ...
                //蛇行步数加1
                walkSteps = walkSteps + 1; //v9
                //刷新消息板
                dispMessage(); //v9
            }       

            function putFood(){ //v2
                ... ...
                //捕食数量计数
                foodNumber = foodNumber + 1; //v9
                //每次捕食后，蛇行步数重新计数
                walkSteps = 0; //v9
            }
            /*
             * 显示游戏状态信息
             */
            function dispMessage(){ //v9
                //显示捕食数量
                foods.innerHTML = foodNumber; //v9
                //显示蛇身长度
                snakes.innerHTML = snakeLength; //v9
                //显示蛇行步数
                steps.innerHTML = walkSteps; //v9
                //显示食物位置
                foodPlace.innerHTML = "(" + foodX*snakeUnitSize + "," + foodY*snakeUnitSize + ")"; //v9
                //显示蛇头位置
                snakePlace.innerHTML = "(" + x + "," + y + ")"; //v9
            }
        </script>
    </head>
    <body>
        <!-- v9 -->
        <center>
            <h2>Greedy Snake</h2>
            <table>
                <tr>
                    <td>
                        <canvas id="field" width="400" height="600">
                            This is the field that snake snaking.
                        </canvas>
                    </td>
                    <td valign="top" align="left">
                        <table class="show">
                            <tr>
                                <td align="right">贪吃蛇长度：</td>
                                <td align="left" id="snakes">35</td>
                            </tr>
                            <tr>
                                <td align="right">捕食数量：</td>
                                <td align="left" id="foods">14</td>
                            </tr>
                            <tr>
                                <td align="right">行走步数：</td>
                                <td align="left" id="steps">1000</td>
                            </tr>
                            <tr>
                                <td align="right">食物位置：</td>
                                <td align="left" id="foodPlace">14</td>
                            </tr>
                            <tr>
                                <td align="right">蛇头位置：</td>
                                <td align="left" id="snakePlace">1000</td>
                            </tr>
                        </table>
                    </td>
                </tr>
            </table>
        </center>
    </body>
</html>
~~~

## 9.5 核心代码

~~~
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Greedy Snake</title>
        <style type="text/css">
            canvas { /*v1*/
                background:#abcdef;
                border:1px solid #000000;
            }
            .show{ /*v9*/
                font-family: "微软雅黑";
                font-size: large;
                font-weight: bold;
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
            var foodNumber = -1; //v9
            var walkSteps = 0; //v9
            var foods; //v9
            var snakes; //v9
            var foodPlace; //v9
            var snakePlace; //v9
            var steps; //v9
            
            window.onload = function(){ //v1
                foods = document.getElementById("foods"); //v9
                snakes = document.getElementById("snakes"); //v9
                steps = document.getElementById("steps"); //v9
                foodPlace = document.getElementById("foodPlace"); //v9
                snakePlace = document.getElementById("snakePlace"); //v9

                field = document.getElementById("field"); //v1
                game = field.getContext("2d"); //v1
                fieldWidth = field.width; //v2
                fieldHeight = field.height; //v2

                putFood(); //v8

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
                
                for(var i=0; i<pathMap.length; i++){ //v7
                    if( parseInt(pathMap[i].x)==x && parseInt(pathMap[i].y)==y){ //v7
                        alert("你挂了，继续努力吧！失败原因：撞到自己了....."); //v7
                        window.location.reload(); //v7
                    } 
                } 

                if (pathMap.length>snakeLength) {  //v6
                    var snakeTail = pathMap.shift(); //v6
                    game.clearRect(snakeTail['x'], snakeTail['y'], snakeUnitSize, snakeUnitSize); //v6
                }
                pathMap.push({'x':x,'y':y}); //v6
                
                game.fillStyle = "#006699"; //v3
                game.strokeStyle = "#006699"; //v3
                game.fillRect(x, y, snakeUnitSize, snakeUnitSize); //v3

                if((foodX*snakeUnitSize)==x && (foodY*snakeUnitSize)==y){ //v8
                    snakeLength++; //v8
                    putFood(); //v8
                }

                walkSteps = walkSteps + 1; //v9
                dispMessage(); //v9
            }       

            function putFood(){ //v2
                var size = snakeUnitSize; //v2
                game.fillStyle = "#ff0000"; //v2
                game.strokeStyle = "#000000"; //v2
                foodX = Math.ceil(Math.random() * (fieldWidth/size)); //v2
                if(foodX*size>fieldWidth-size) //v8
                    foodX = foodX - 1; //v8
                foodY = Math.ceil(Math.random() * (fieldHeight/size)); //v2
                if(foodY*size>fieldHeight-size) //v8
                    foodY = foodY - 1; //v8
                game.fillRect(foodX*size, foodY*size, size, size); //v2

                foodNumber = foodNumber + 1; //v9
                walkSteps = 0; //v9
            }

            function dispMessage(){ //v9
                foods.innerHTML = foodNumber; //v9
                snakes.innerHTML = snakeLength; //v9
                steps.innerHTML = walkSteps; //v9
                foodPlace.innerHTML = "(" + foodX*snakeUnitSize + "," + foodY*snakeUnitSize + ")"; //v9
                snakePlace.innerHTML = "(" + x + "," + y + ")"; //v9
            }
        </script>
    </head>
    <body>
        <center> <!-- v9 -->
            <h2>Greedy Snake</h2>
            <table>
                <tr>
                    <td>
                        <canvas id="field" width="400" height="600">
                            This is the field that snake snaking.
                        </canvas>
                    </td>
                    <td valign="top" align="left">
                        <table class="show">
                            <tr>
                                <td align="right">贪吃蛇长度：</td>
                                <td align="left" id="snakes">35</td>
                            </tr>
                            <tr>
                                <td align="right">捕食数量：</td>
                                <td align="left" id="foods">14</td>
                            </tr>
                            <tr>
                                <td align="right">行走步数：</td>
                                <td align="left" id="steps">1000</td>
                            </tr>
                            <tr>
                                <td align="right">食物位置：</td>
                                <td align="left" id="foodPlace">14</td>
                            </tr>
                            <tr>
                                <td align="right">蛇头位置：</td>
                                <td align="left" id="snakePlace">1000</td>
                            </tr>
                        </table>
                    </td>
                </tr>
            </table>
        </center>
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
