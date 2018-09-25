# 3. 贪吃蛇版本迭代（V3） 

- 张大为
- 辽宁师范大学计算机与信息技术学院@大连
- [https://daweizh.github.io/h5/](https://daweizh.github.io/h5/)  QQ:1243605845

## 3.1 需求说明

- 初始化食物大小（和蛇节大小相同）snakeUnitSize，默认值为8
- 获取游戏场景大小fieldWidth和fieldHeight
- 计算食物随机投放的网格位置foodX和foodY，默认值为（0,0）
- 间隔speed（默认值160ms）后，putFood投放食物

## 3.2 效果设计

![效果图](demo.png)

## 3.3 编程过程

1. 在window.onload中删除代码
    ~~~
    game.fillStyle = "#ff0000";
    game.strokeStyle = "#000000";
    game.fillRect(100, 100, 8, 8);
    ~~~
2. 在window.onload中增加代码
	~~~
    fieldWidth = field.width;
    fieldHeight = field.height;
    window.setInterval(putFood, speed);
	~~~
3. 增加投放食物功能
	~~~
    function putFood(){
        var size = snakeUnitSize;
        game.fillStyle = "#ff0000";
        game.strokeStyle = "#000000";
        foodX = Math.ceil(Math.random() * (fieldWidth/size));
        foodY = Math.ceil(Math.random() * (fieldHeight/size));
        game.fillRect(foodX*size, foodY*size, size, size);
    } 
	~~~

## 3.4 代码注解

~~~
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Greedy Snake</title>
        <style type="text/css">
            div {
                width:400px;
                margin:0 auto;  
            }
            canvas {
                background:#abcdef;
                border:1px solid #000000;
            }
        </style>
        <script type="text/javascript">
            var field;
            var game;
            //游戏场景宽度
            var fieldWidth;
            //游戏场景高度
            var fieldHeight;
            //蛇行走的速度
            var speed = 160;
            //食物的最初位置
            var foodX = foodY = 0;
            //蛇节的大小，也是食物的大小
            var snakeUnitSize = 8;
            
            window.onload = function(){
                field = document.getElementById("field");
                game = field.getContext("2d");
                //game.fillStyle = "#ff0000";
                //game.strokeStyle = "#000000";
                //game.fillRect(100, 100, 8, 8);
                //得到游戏场景的宽度
                fieldWidth = field.width;
                //得到游戏场景的高度
                fieldHeight = field.height;
                //固定时间间隔执行，每隔speed毫秒执行putFood功能
                window.setInterval(putFood, speed);
            }

            /* 
             * 随机投放食物
             * Math.ceil小数向上取证，如10.1得到11
             * Math.random()得到0.0~1.0之间的一个伪随机数。
             * fieldWidth/size计算横向网格数
             * fieldHeight/size计算纵向网格数
             */
            function putFood(){
                //得到食物的大小
                var size = snakeUnitSize;
                //设置食物内部颜色
                game.fillStyle = "#ff0000";
                //设置食物边框颜色
                game.strokeStyle = "#000000";
                //计算食物在场景网格的x坐标
                foodX = Math.ceil(Math.random() * (fieldWidth/size));
                //计算食物在场景网格的y坐标
                foodY = Math.ceil(Math.random() * (fieldHeight/size));
                //计算食物的具体坐标，绘制食物
                game.fillRect(foodX*size, foodY*size, size, size);
            } 
        </script>
    </head>
    <body>
        <h2 align="center">Greedy Snake</h2>
        <div>
            <canvas id="field" width="400" height="600">
                This is the field that snake snaking.
            </canvas>
        </div>
    </body>
</html>
~~~

## 3.5 核心代码

~~~
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Greedy Snake</title>
        <style type="text/css">
            div {
                width:400px;
                margin:0 auto;  
            }
            canvas {
                background:#abcdef;
                border:1px solid #000000;
            }
        </style>
        <script type="text/javascript">
            var field;
            var game;
            var fieldWidth;
            var fieldHeight;
            var speed = 160;
            var foodX = foodY = 0;
            var snakeUnitSize = 8;
            
            window.onload = function(){
                field = document.getElementById("field");
                game = field.getContext("2d");
                fieldWidth = field.width;
                fieldHeight = field.height;
                window.setInterval(putFood, speed);
            }

            function putFood(){
                var size = snakeUnitSize;
                game.fillStyle = "#ff0000";
                game.strokeStyle = "#000000";
                foodX = Math.ceil(Math.random() * (fieldWidth/size));
                foodY = Math.ceil(Math.random() * (fieldHeight/size));
                game.fillRect(foodX*size, foodY*size, size, size);
            } 
        </script>
    </head>
    <body>
        <h2 align="center">Greedy Snake</h2>
        <div>
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

## b.[返回首页](../../)

