# 1. 贪吃蛇版本迭代（V1） 

- 张大为
- 辽宁师范大学计算机与信息技术学院@大连
- [https://daweizh.github.io/h5/](https://daweizh.github.io/h5/)  QQ:1243605845

## 1.1 需求说明

- 初始化游戏场景
- 在坐标(100,100)处放置大小为8x8的食物

## 1.2 效果设计

![效果图](demo.png)

## 1.3 编程过程

1. 修改网页标题
    ~~~html
    <title>Greedy Snake</title>
    ~~~
2. 增加游戏标题
	~~~html
	<h2 align="center">Greedy Snake</h2>
	~~~
3. 增加游戏场景
	~~~html
    <div>
        <canvas id="field" width="400" height="600">
            This is the field that snake snaking.
        </canvas>
    </div>
	~~~
4. 改变场景样式
	~~~html
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
	~~~
5. 绘制食物
	~~~html
    <script type="text/javascript">
        var field;
        var game;
        window.onload = function(){
            field = document.getElementById("field");
            game = field.getContext("2d");
            game.fillStyle = "#ff0000";
            game.strokeStyle = "#000000";
            game.fillRect(100, 100, 8, 8);
        }
    </script>
	~~~

## 1.4 代码注解

~~~html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Greedy Snake</title>
        <style type="text/css">
            /*直接对div标记规定样式*/
            div {
                width:400px;
                /*上下边界为0，左右边界自适应*/
                margin:0 auto;  
            }
            /*直接对canvas标记规定样式*/
            canvas {
                background:#abcdef;
                border:1px solid #000000;
            }
        </style>
        <script type="text/javascript">
            /*定义canvas对象变量*/
            var field;
            /*field环境对象，用来执行各种绘制行为*/
            var game;
            /*当所有网页内容加载完成后执行*/
            window.onload = function(){
                /*获取网页中的canvas对象*/
                field = document.getElementById("field");
                /*得到canvas对象field所创建的绘制环境对象*/
                game = field.getContext("2d");
                /*填充颜色，红色*/
                game.fillStyle = "#ff0000";
                /*线条颜色*/
                game.strokeStyle = "#000000";
                /*填充绘制一个方块（食物）*/
                game.fillRect(100, 100, 8, 8);
            }
        </script>
    </head>
    <body>
        <!-- 标题是如何居中的？ -->
        <h2 align="center">Greedy Snake</h2>
        <!-- 画布时如何居中的？ -->
        <div>
            <!-- 画布的样式是如何改变的？ -->
            <canvas id="field" width="400" height="600">
                This is the field that snake snaking.
            </canvas>
        </div>
    </body>
</html>
~~~

## 1.5 核心代码

~~~html
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
            window.onload = function(){
                field = document.getElementById("field");
                game = field.getContext("2d");
                game.fillStyle = "#ff0000";
                game.strokeStyle = "#000000";
                game.fillRect(100, 100, 8, 8);
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

## b.[返回](../)

## t.[首页](../../)

