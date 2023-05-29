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

const imgUrl = new URL('./assets/texture/backsword.png', import.meta.url).href
const texture = PIXI.Texture.from(imgUrl)
//创建一个精灵
const sprite = new PIXI.Sprite(texture)
app.stage.addChild(sprite)

//创建模糊滤镜
const blurFilter = new PIXI.BlurFilter()
//修改模糊滤镜的模糊程度
blurFilter.blur = 10
//添加到sprite
sprite.filters = [blurFilter]
sprite.interactive = true

//OutlineFilter需要安装
//
//创建轮廓滤镜  轮廓宽度  轮廓颜色
const outlineFilter = new OutlineFilter(5, 0xffff00)

//创建发光滤镜
const glowFilter = new GlowFilter({
  distance: 50,
  outerStrength: 5,
  innerStrength: 0,
  color: 0xff0000,
  quality: 0.5
})

//监听鼠标是否移入
sprite.on('pointerenter', () => {
  sprite.filters = [blurFilter, outlineFilter, glowFilter]
  blurFilter.blur = 0
})
sprite.on('pointerout', () => {
  sprite.filters = [blurFilter]
  blurFilter.blur = 10
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
