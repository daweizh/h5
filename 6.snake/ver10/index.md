# 10. 贪吃蛇版本迭代（V10） 

- 张大为
- 辽宁师范大学计算机与信息技术学院@大连
- [https://daweizh.github.io/h5/](https://daweizh.github.io/h5/)  QQ:1243605845

## 10.1 需求说明

- 增加减速功能键a
- 增加加速功能键d
- 增加对准功能键w；放开蛇行缠绕的判断，使蛇头可以穿越自己
- 增加游戏说明布局

## 10.2 效果设计

![效果图](demo.png)

## 10.3 编程过程

1. 增加游戏说明布局
    ~~~html
    <td valign="top" align="left" width="300px">
        <table>
            <tr><th>玩法说明</th></tr>
            <tr><td>
                <ol>
                    <li>上下左右方向键，改变蛇行方向</li>
                    <li>蛇头超出边界，游戏结束</li>
                    <li>沙头撞到自身，游戏结束</li>
                    <li>每捕捉到一个食物，蛇身长长一节</li>
                    <li>a键减慢蛇行速度</li>
                    <li>d键加快蛇行速度</li>
                    <li>w键标注线和自身缠绕开关</li>
                </ol>
            </td></tr>
        </table>
    </td>
    ~~~
2. 修改游戏状态信息栏宽度
    ~~~html
    <td valign="top" align="left" width="300px">
    ~~~
3. 设置游戏`power`变量
    ~~~js
    var oldX = oldY = snakeUnitSize;
    var power = 0;
    var heartbeat;
    var snakeSpeed;
    ~~~
4. 增加速度显示栏，在`window.onload`中增加
    ~~~js
    snakeSpeed = document.getElementById("snakeSpeed");
    ~~~
    修改
    ~~~js
    window.setInterval(snakeMove, speed);
    ~~~
    为
    ~~~js
    heartbeat = window.setInterval(snakeMove, speed);
    ~~~
    在`dispMessage`方法中增加
    ~~~js
    snakeSpeed.innerHTML = speed;
    ~~~
5. 在`document.onkeydown`事件中增加a键减速功能
    ~~~js
    case 28: //a
        speed = speed + 10;
        window.clearInterval(heartbeat);
        heartbeat=window.setInterval(snakeMove, speed);
        break;
    ~~~
6. 在`document.onkeydown`事件中增加d键加速功能
    ~~~js
    case 31: //d
        speed = speed - 10;
        if (speed<50) speed = 50;
        window.clearInterval(heartbeat);
        heartbeat=window.setInterval(snakeMove, speed);
        break;
    ~~~
7. 在`document.onkeydown`事件中增加w键校准开关
    ~~~js
    case 50: //w
        if(power==0)
            power = 1;
        else
            power = 0;
        break;
    ~~~
8. 在 `snakeMove`方法中记录蛇头刚刚走过的位置
    ~~~js
    oldX = x; //v10
    oldY = y; //v10
    ~~~
    增加蛇头穿越自身能力
    ~~~js
    if(power==0){
        for(var i=0; i<pathMap.length; i++){ //v7
            if( parseInt(pathMap[i].x)==x && parseInt(pathMap[i].y)==y){ //v7
                alert("你挂了，继续努力吧！失败原因：撞到自己了....."); //v7
                window.location.reload(); //v7
            } 
        } 
    }
    ~~~
    增加超级校准线能力
    ~~~js
    if(power==1)
        showPower();
    ~~~
9. 增加超级能力“校准线”功能
    ~~~js
    function showPower(){
        game.lineWidth = 2;
        game.strokeStyle = "#abcdef";

        game.beginPath();
        game.moveTo(oldX,oldY);
        game.lineTo(foodX * snakeUnitSize,foodY * snakeUnitSize);
        game.stroke();
        
        game.strokeStyle = "#f0f0f0";
        game.lineWidth = 1;
        game.beginPath();
        game.moveTo(x,y);
        game.lineTo(foodX * snakeUnitSize,foodY * snakeUnitSize);
        game.stroke();
    }
    ~~~        
    
## 10.4 代码注解

~~~html
<script type="text/javascript">
    ... ...
    //蛇行速度消息栏对象
    var snakeSpeed; //v10
    //为绘制校准标注线，保存蛇头刚移动过的位置坐标
    var oldX = oldY = snakeUnitSize; //v10
    //超级功能“校准线”开关
    var power = 0; //v10
    //保存定时器对象
    var heartbeat; //v10

    window.onload = function(){ //v1
        ... ...
        //获取蛇行速度信息栏对象
        snakeSpeed = document.getElementById("snakeSpeed"); //v10
        ... ...
        //保存定时器对象
        heartbeat = window.setInterval(snakeMove, speed); //v3，v10
    }

    document.onkeydown = function(e) { //v5
        var code = e.keyCode - 37; //v5
        //alert(code);
        switch(code){ //v5
            ... ...
            case 28: //a //v10
                //每按一次a键速度减慢10毫秒
                speed = speed + 10; //v10
                //清除前一个定时器
                window.clearInterval(heartbeat); //v10
                //用新速度设定新定时器
                heartbeat=window.setInterval(snakeMove, speed); //v10
                break;
            case 31: //d //v10
                //每按一次d键速度加快10毫秒
                speed = speed - 10; //v10
                //设置最快速度的最短时间间隔
                if (speed<50) speed = 50; //v10
                //清除前一个定时器
                window.clearInterval(heartbeat); //v10
                //用新速度设置新定时器
                heartbeat=window.setInterval(snakeMove, speed); //v10
                break;
            case 50: //w
                //如果超级校准功能未开
                if(power==0) //v10
                    //打开超级校准功能
                    power = 1; //v10
                else
                    //关闭超级校准功能
                    power = 0; //v10
                break;
        } 
    } 

    function snakeMove(){ //v3
        oldX = x;
        oldY = y;
        ... ...
        if(power==0){
            for(var i=0; i<pathMap.length; i++){ //v7
                if( parseInt(pathMap[i].x)==x && parseInt(pathMap[i].y)==y){ //v7
                    alert("你挂了，继续努力吧！失败原因：撞到自己了....."); //v7
                    window.location.reload(); //v7
                } 
            } 
        }
        ... ...
        //如果超级校准功能已经打开
        if(power==1) //v10
            //显示超级校准功能
            showPower(); //v10
        ... ...
    }       

    ... ...
    
    function dispMessage(){ //v9
        ... ...
        //刷新蛇行速度状态信息
        snakeSpeed.innerHTML = speed; //v10
    }

    /*
     * 绘制超级功能“校准线”
     */
    function showPower(){ //v10
        //设置擦除线宽为2
        game.lineWidth = 2; //v10
        //设置擦除线颜色为背景颜色
        game.strokeStyle = "#abcdef"; //v10
        
        //开始绘制线条
        game.beginPath(); //v10
        //移动坐标到蛇头刚走过的位置
        game.moveTo(oldX,oldY); //v10
        //清除到食物的旧线
        game.lineTo(foodX * snakeUnitSize,foodY * snakeUnitSize); //v10
        //清除绘制完成
        game.stroke(); //v10
        
        //设置超级校准线的颜色为浅灰色
        game.strokeStyle = "#f0f0f0"; //v10
        //设计线宽为1
        game.lineWidth = 1; //v10
        //开始绘制超级校准线
        game.beginPath(); //v10
        //设置线段起始坐标为蛇头新到位置
        game.moveTo(x,y); //v10
        //绘制到食物的线段
        game.lineTo(foodX * snakeUnitSize,foodY * snakeUnitSize); //v10
        //绘制完成
        game.stroke(); //v10
    }
</script>
... ...
<center>
    <h2>Greedy Snake</h2>
    <table>
        <tr>
            <!-- v10 增加游戏玩法说明栏 -->
            <td valign="top" align="left" width="300px">
                <table>
                    <tr><th>玩法说明</th></tr>
                    <tr><td>
                        <ol>
                            <li>上下左右方向键，改变蛇行方向</li>
                            <li>蛇头超出边界，游戏结束</li>
                            <li>沙头撞到自身，游戏结束</li>
                            <li>每捕捉到一个食物，蛇身长长一节</li>
                            <li>a键减慢蛇行速度</li>
                            <li>d键加快蛇行速度</li>
                            <li>w键标注线和自身缠绕开关</li>
                        </ol>
                    </td></tr>
                </table>
            </td>
            <td width="400px">
            ...
            </td>
            <td valign="top" align="left" width="300px">
            ... ...
            </td>
        </tr>
    </table>
</center>
~~~

## 10.5 核心代码

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
            .show{ /*v10*/
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
            
            var snakeSpeed; //v10
            var oldX = oldY = snakeUnitSize; //v10
            var power = 0; //v10
            var heartbeat; //v10

            window.onload = function(){ //v1
                foods = document.getElementById("foods"); //v9
                snakes = document.getElementById("snakes"); //v9
                steps = document.getElementById("steps"); //v9
                foodPlace = document.getElementById("foodPlace"); //v9
                snakePlace = document.getElementById("snakePlace"); //v9
                snakeSpeed = document.getElementById("snakeSpeed"); //v10

                field = document.getElementById("field"); //v1
                game = field.getContext("2d"); //v1
                fieldWidth = field.width; //v2
                fieldHeight = field.height; //v2

                putFood(); //v8

                heartbeat = window.setInterval(snakeMove, speed); //v3，v10
            }

            document.onkeydown = function(e) { //v5
                var code = e.keyCode - 37; //v5
                //alert(code);
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
                    case 28: // //v10a
                        speed = speed + 10; //v10
                        window.clearInterval(heartbeat); //v10
                        heartbeat=window.setInterval(snakeMove, speed); //v10
                        break;
                    case 31: //d //v10
                        speed = speed - 10; //v10
                        if (speed<50) speed = 50; //v10
                        window.clearInterval(heartbeat); //v10
                        heartbeat=window.setInterval(snakeMove, speed); //v10
                        break;
                    case 50: //w //v10
                        if(power==0) //v10
                            power = 1; //v10
                        else
                            power = 0; //v10
                        break;
                } 
            } 

            function snakeMove(){ //v3
                oldX = x; //v10
                oldY = y; //v10
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
                
                if(power==0){ //v10
                    for(var i=0; i<pathMap.length; i++){ //v7
                        if( parseInt(pathMap[i].x)==x && parseInt(pathMap[i].y)==y){ //v7
                            alert("你挂了，继续努力吧！失败原因：撞到自己了....."); //v7
                            window.location.reload(); //v7
                        } 
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

                game.fillStyle = "#ff0000"; //v2
                game.strokeStyle = "#000000"; //v2
                game.fillRect(foodX*snakeUnitSize, foodY*snakeUnitSize, snakeUnitSize, snakeUnitSize); //v2

                if(power==1) //v10
                    showPower(); //v10
                
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
                snakeSpeed.innerHTML = speed; //v10
            }

            function showPower(){ //v10
                game.lineWidth = 2; //v10
                game.strokeStyle = "#abcdef"; //v10

                game.beginPath(); //v10
                game.moveTo(oldX,oldY); //v10
                game.lineTo(foodX * snakeUnitSize,foodY * snakeUnitSize); //v10
                game.stroke(); //v10
                
                game.strokeStyle = "#f0f0f0"; //v10
                game.lineWidth = 1; //v10
                game.beginPath(); //v10
                game.moveTo(x,y); //v10
                game.lineTo(foodX * snakeUnitSize,foodY * snakeUnitSize); //v10
                game.stroke(); //v10
            }
        </script>
    </head>
    <body>
        <center>
            <h2>Greedy Snake</h2>
            <table>
                <tr>
                    <td valign="top" align="left" width="300px">
                        <table>
                            <tr><th>玩法说明</th></tr>
                            <tr><td>
                                <ol>
                                    <li>上下左右方向键，改变蛇行方向</li>
                                    <li>蛇头超出边界，游戏结束</li>
                                    <li>沙头撞到自身，游戏结束</li>
                                    <li>每捕捉到一个食物，蛇身长长一节</li>
                                    <li>a键减慢蛇行速度</li>
                                    <li>d键加快蛇行速度</li>
                                    <li>w键标注线和自身缠绕开关</li>
                                </ol>
                            </td></tr>
                        </table>
                    </td>
                    <td width="400px">
                        <canvas id="field" width="400" height="600">
                            This is the field that snake snaking.
                        </canvas>
                    </td>
                    <td valign="top" align="left" width="300px">
                        <table class="show">
                            <tr>
                                <td align="right" nowrap="nowrap">贪吃蛇长度：</td>
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
                            <tr>
                                <td align="right">行走速度：</td>
                                <td align="left" id="snakeSpeed">1000</td>
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
