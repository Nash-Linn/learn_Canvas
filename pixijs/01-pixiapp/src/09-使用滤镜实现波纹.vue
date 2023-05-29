<template>
  <div></div>
</template>
<script setup>
import * as PIXI from 'pixi.js'
import { ShockwaveFilter } from 'pixi-filters'
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

//添加置换滤镜
const displacementSprite = PIXI.Sprite.from(
  new URL('./assets/displacement.png', import.meta.url).href
)
displacementSprite.scale.set(5)
displacementSprite.texture.baseTexture.wrapMode = PIXI.WRAP_MODES.REPEAT
const displacementFilter = new PIXI.DisplacementFilter(displacementSprite)

container.addChild(displacementSprite)

//添加震波滤镜
const shockwaveFilter1 = new ShockwaveFilter(
  [Math.random() * app.screen.width, Math.random() * app.screen.height],
  {
    amplitude: 70, //振幅
    wavelength: 100, //波长
    speed: 160, //速度
    radius: 80 //半径
  }
)

const shockwaveFilter2 = new ShockwaveFilter(
  [Math.random() * app.screen.width, Math.random() * app.screen.height],
  {
    amplitude: 80, //振幅
    wavelength: 45, //波长
    speed: 240, //速度
    radius: 100 //半径
  }
)

const shockwaveFilter3 = new ShockwaveFilter(
  [Math.random() * app.screen.width, Math.random() * app.screen.height],
  {
    amplitude: 105, //振幅
    wavelength: 65, //波长
    speed: 300, //速度
    radius: 160 //半径
  }
)

container.filters = [displacementFilter, shockwaveFilter1, shockwaveFilter2, shockwaveFilter3]

app.ticker.add(() => {
  displacementSprite.x++
  displacementSprite.y++
  createWave(shockwaveFilter1, 1)
  createWave(shockwaveFilter2, 1.2)
  createWave(shockwaveFilter3, 0.7)
})

function createWave(waveFilter, resetTime) {
  waveFilter.time += 0.01
  if (waveFilter.time > resetTime) {
    waveFilter.time = 0
    waveFilter.center = [Math.random() * app.screen.width, Math.random() * app.screen.height]
  }
}

//监听点击事件，根据位置创建波纹
app.view.addEventListener('click', (e) => {
  shockwaveFilter3.center = [e.clientX, e.clientY]
  shockwaveFilter3.time = 0
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
