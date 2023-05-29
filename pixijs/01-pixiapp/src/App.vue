<template>
  <div></div>
</template>
<script setup>
import * as PIXI from 'pixi.js'
import { OutlineFilter, GlowFilter } from 'pixi-filters'

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

//创建一个纹理
//在vite中引入静态资源需要使用 new URL()
const imgUrl = new URL('./assets/background.png', import.meta.url).href
const texture = PIXI.Texture.from(imgUrl)

//创建一个精灵
const sprite = new PIXI.Sprite(texture)
sprite.width = app.screen.width
sprite.height = app.screen.height

//创建容器
const container = new PIXI.Container()
//将精灵添加到容器中
container.addChild(sprite)
//将容器添加到舞台
app.stage.addChild(container)

//添加文字
const text = new PIXI.Text('Hello PixiJS', {
  fontFamily: 'Arial',
  fontSize: 30 + Math.floor(app.screen.width * 0.1),
  fill: 0xffffff,
  align: 'center',
  dropShadow: true,
  dropShadowColor: '#000000',
  drorShadowBlur: 4,
  dropShadowAngle: Math.PI / 2,
  dropShadowDistance: 20
})
text.x = app.screen.width / 2
text.y = app.screen.height / 2
text.anchor.set(0.5)
container.addChild(text)
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
