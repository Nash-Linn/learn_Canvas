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

//添加资源
const addAssets = (name) => {
  const imgUrl = new URL(`./assets/texture/${name}.png`, import.meta.url).href
  PIXI.Assets.add(name, imgUrl)
}
addAssets('backsword')
addAssets('man')

// 异步加载资源
const texturesPromise = PIXI.Assets.load(['backsword', 'man'], (progress) => {
  console.log('progress', progress)
})

// 加载完成后创建精灵
texturesPromise.then((textures) => {
  //创建容器
  const container = new PIXI.Container()
  //创建精灵
  const sprite_backsword = new PIXI.Sprite(textures.backsword)
  //设置精灵的位置
  sprite_backsword.x = app.screen.width / 2
  sprite_backsword.y = app.screen.height / 2
  //设置精灵旋转45度
  sprite_backsword.rotation = Math.PI / 4
  //设置精灵的缩放
  sprite_backsword.scale.set(0.5, 0.5)
  //设置精灵的透明度
  sprite_backsword.alpha = 0.5
  container.addChild(sprite_backsword)
  //ticker实现动画
  app.ticker.add((delta) => {
    sprite_backsword.rotation += 0.01 * delta
  })
  //为精灵添加点击事件
  sprite_backsword.interactive = true
  sprite_backsword.on('click', () => {
    console.log('click sprite')
  })
  //鼠标进入
  sprite_backsword.on('pointerenter', () => {
    sprite_backsword.alpha = 1
  })
  //鼠标离开
  sprite_backsword.on('pointerout', () => {
    sprite_backsword.alpha = 0.5
  })

  //创建精灵
  const sprite_man = new PIXI.Sprite(textures.man)
  //设置精灵的位置
  sprite_man.x = app.screen.width / 2
  sprite_man.y = app.screen.height / 2
  //ticker实现动画
  container.addChild(sprite_man)

  app.stage.addChild(container)
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
