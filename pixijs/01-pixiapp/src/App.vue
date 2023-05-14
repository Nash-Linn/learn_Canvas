<template>
  <div></div>
</template>
<script setup>
import * as PIXI from 'pixi.js'

//创建应用
const app = new PIXI.Application({
  width: window.innerWidth,
  height: window.innerHeight,
  backgroundColor: 0x1099bb,
  resolution: window.devicePixelRatio || 1,
  antialias: true //抗锯齿
})

//将应用画布添加到dom中
document.body.appendChild(app.view)

//创建一个矩形
const rectangle = new PIXI.Graphics()
//填充颜色
//参数1 颜色
//参数2 透明度
rectangle.beginFill(0x66ccff, 0.5)

//设置边框样式 （线宽,颜色,透明度)
rectangle.lineStyle(4, 0xff0000, 1)

rectangle.drawRect(100, 100, 100, 50) //绘制矩形

//结束填充
rectangle.endFill()

//图像的缩放
rectangle.scale.set(2, 2)

//图像的位移
rectangle.position.set(100, 100)

//设置锚点
rectangle.pivot.set(100, 100)

//图形的旋转
rectangle.rotation = 0.5

//将矩形添加到舞台
app.stage.addChild(rectangle)

//创建一个圆形
const circle = new PIXI.Graphics()
circle.beginFill(0x66ccff, 0.9)
circle.drawCircle(0, 0, 32)
circle.endFill()
circle.position.set(100, 300)
app.stage.addChild(circle)

//绘制圆角矩形
const roundRectangle = new PIXI.Graphics()
roundRectangle.beginFill(0x66ccff, 0.9)
roundRectangle.drawRoundedRect(0, 0, 100, 50, 10)
roundRectangle.endFill()
roundRectangle.position.set(100, 500)
app.stage.addChild(roundRectangle)

//绘制椭圆
const ellipse = new PIXI.Graphics()
ellipse.beginFill(0x66ccff, 0.9)
ellipse.drawEllipse(0, 0, 100, 50)
ellipse.endFill()
ellipse.position.set(300, 100)
app.stage.addChild(ellipse)

//绘制多边形
const polygon = new PIXI.Graphics()
polygon.beginFill(0x66ccff, 0.9)
polygon.drawPolygon([0, 0, 100, 0, 120, 100, 0, 100, -50, 50]) //数组中每两个元素分别对应x,y
polygon.endFill()
polygon.position.set(300, 300)
app.stage.addChild(polygon)

//绘制圆弧
const arc = new PIXI.Graphics()
arc.beginFill(0x66ccff, 0.9)
// (x,y,半径,起始角度,结束角度,是否逆时针)
arc.arc(0, 0, 32, 0, Math.PI, false)
arc.position.set(300, 500)
app.stage.addChild(arc)

//绘制线段
const line = new PIXI.Graphics()
line.lineStyle(4, 0x66ccff, 0.9)
line.moveTo(0, 0) //线段起点
line.lineTo(100, 100) //线段终点
line.lineTo(100, 50) //线段终点
line.position.set(500, 100)
app.stage.addChild(line)
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

canvas {
  width: 100vw;
  height: 100vh;
  position: fixed;
  left: 0;
  top: 0;
}
</style>
