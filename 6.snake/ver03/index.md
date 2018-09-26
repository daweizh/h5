# 3. 贪吃蛇版本迭代（V3） 

- 张大为
- 辽宁师范大学计算机与信息技术学院@大连
- [https://daweizh.github.io/h5/](https://daweizh.github.io/h5/)  QQ:1243605845

## 3.1 需求说明

- 初始化蛇头开始出没的位置坐标(x,y)，默认值为snakeUnitSize
- 让蛇动起来，间隔speed（默认值160ms）后，snakeMove蛇头前进一步

## 3.2 效果设计

![效果图](demo.png)

## 3.3 编程过程

1. 增加蛇头坐标全局变量
    ~~~
    var x = y = snakeUnitSize;
    ~~~
2. 在window.onload中，修改代码
	~~~
    window.setInterval(putFood, speed);
	~~~
	为
	~~~
	window.setInterval(snakeMove, speed);
	~~~
3. 增加蛇头水平向右行走代码
	~~~
    function snakeMove(){
        x = x + snakeUnitSize;
        game.fillStyle = "#006699";
        game.strokeStyle = "#006699"; 
        game.fillRect(x, y, snakeUnitSize, snakeUnitSize);
    }       
	~~~

## 3.4 代码注解

~~~
<script type="text/javascript">
    // v1 ... v2
    //蛇最开始出没的地方
    var x = y = snakeUnitSize; //v3

    window.onload = function(){ //v1
        //v1 ... v2
        //window.setInterval(putFood, speed); //v2
        //固定时间间隔执行，每隔speed毫秒执行snakeMove功能
        window.setInterval(snakeMove, speed); //v3
    }

    /*
     * 让蛇运动的功能，每次走一个蛇身单位
     */
    function snakeMove(){ //v3
        //每次水平方向移动一个蛇节
        x = x + snakeUnitSize; //v3
        //内部填充颜色
        game.fillStyle = "#006699"; //v3
        //边框颜色
        game.strokeStyle = "#006699"; //v3
        //根据新得到的蛇头绘制位置，绘制蛇头
        game.fillRect(x, y, snakeUnitSize, snakeUnitSize); //v3
    }       

</script>
~~~

## 3.5 核心代码

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

            window.onload = function(){ //v1
                field = document.getElementById("field"); //v1
                game = field.getContext("2d"); //v1
                fieldWidth = field.width; //v2
                fieldHeight = field.height; //v2
                window.setInterval(snakeMove, speed); //v3
            }

            function snakeMove(){ //v3
                x = x + snakeUnitSize; //v3
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

## b.[返回首页](../../)

