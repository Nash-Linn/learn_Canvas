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

//显示hello world 文字
const text = new PIXI.Text('Hello world', {
  fontFamily: 'Arial',
  fontSize: 150,
  fill: 'white',
  align: 'center'
})
//设置文字位置
text.x = app.screen.width / 2
text.y = app.screen.height / 2
//设置锚点
text.anchor.set(0.5)
app.stage.addChild(text)

//创建一个圆
const circle = new PIXI.Graphics()
circle.beginFill(0x0000ff)
circle.drawCircle(0, 0, 100)
circle.endFill()
circle.x = app.screen.width / 2
circle.y = app.screen.height / 2 + 200
app.stage.addChild(circle)
//创建一个精灵
const imgUrl = new URL('./assets/background.png', import.meta.url).href
const bunny = PIXI.Sprite.from(imgUrl)
//让精灵铺满整个屏幕
bunny.width = app.screen.width
bunny.height = app.screen.height
//使用文字作为精灵的遮罩
bunny.mask = text
// bunny.mask = circle
app.stage.addChild(bunny)
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
