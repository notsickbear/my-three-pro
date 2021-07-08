<template>
  <div id='sample-three' ref='sampleThree' />
</template>

<script lang='ts'>
import {defineComponent, onMounted, ref} from 'vue'
import {BoxGeometry, DirectionalLight, Mesh, MeshLambertMaterial, PerspectiveCamera, Scene, WebGLRenderer} from 'three'

export default defineComponent({
  name: 'SampleThreeView',
  mounted () {
    const dom = this.$refs.sampleThree
    // 场景
    const scene = new Scene()
    // 透视摄像机
    const camera = new PerspectiveCamera(75, window.innerWidth / window.innerHeight,
        0.1, 1000)
    // 渲染器
    const renderer = new WebGLRenderer()
    renderer.setSize(dom.clientWidth, dom.clientHeight)
    dom.appendChild(renderer.domElement)
    /* 立方体 */
    const geometry = new BoxGeometry(1, 1, 1)
    const material = new MeshLambertMaterial()
    const cube = new Mesh(geometry, material)
    // 物体将会被添加到(0,0,0)坐标
    scene.add(cube)
    // 将摄像机稍微向外移动一些
    camera.position.z = 5
    /* 平行光 */
    const light = new DirectionalLight(0xff0000, 1)
    light.position.set(0, 10, 5)
    scene.add(light)
    /* 渲染循环 */
    const animate = () => {
      requestAnimationFrame(animate)
      cube.rotation.x += 0.01
      cube.rotation.y += 0.01
      // 渲染
      renderer.render(scene, camera)
    }
    animate()
  }
})
</script>

<style scoped>
#sample-three {
  width: 70%;
  height: 70%;
}
</style>