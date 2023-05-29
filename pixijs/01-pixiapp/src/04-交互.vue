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

//创建一个纹理
//在vite中引入静态资源需要使用 new URL()
const imgUrl = new URL('./assets/texture/backsword.png', import.meta.url).href
const texture = PIXI.Texture.from(imgUrl)

//创建一个精灵
const sprite = new PIXI.Sprite(texture)

//设置精灵的位置
sprite.x = app.screen.width / 2
sprite.y = app.screen.height / 2

//设置精灵旋转45度
sprite.rotation = Math.PI / 4

//设置精灵的缩放
sprite.scale.set(0.5, 0.5)

//设置精灵的透明度
sprite.alpha = 0.5

app.stage.addChild(sprite)

//ticker实现动画
app.ticker.add((delta) => {
  sprite.rotation += 0.01 * delta
})

//为精灵添加点击事件
sprite.interactive = true
sprite.on('click', () => {
  console.log('click sprite')
})

//鼠标进入
sprite.on('pointerenter', () => {
  sprite.alpha = 1
})

//鼠标离开
sprite.on('pointerout', () => {
  sprite.alpha = 0.5
})

// 绘制一个矩形
const rect = new PIXI.Graphics()
rect.beginFill(0xff0000)
rect.drawRect(0, 0, 100, 100)
rect.endFill()
rect.x = 100
rect.y = 100
app.stage.addChild(rect)

//给矩形添加交互事件
rect.interactive = true
rect.on('click', () => {
  console.log('click rect')
  //ticker实现动画
  app.ticker.add((delta) => {
    rect.rotation += 0.01 * delta
  })
})
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
