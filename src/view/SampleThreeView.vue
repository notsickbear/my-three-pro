<template>
  <div id='sample-three' ref='sampleThree' />
</template>

<script lang='ts'>
import {defineComponent, onMounted, ref} from 'vue'
import {
  AmbientLight,
  BoxGeometry,
  DirectionalLight,
  Mesh,
  MeshLambertMaterial,
  PerspectiveCamera,
  PointLight,
  Scene,
  WebGLRenderer
} from 'three'

export default defineComponent({
  name: 'SampleThreeView',
  mounted () {
    const dom = this.$refs.sampleThree
    /* 场景 */
    const scene = new Scene()
    /* 透视摄像机 */
    const camera = new PerspectiveCamera(75, window.innerWidth / window.innerHeight,
        0.1, 1000)
    // 将摄像机稍微向外移动一些
    camera.position.z = 5
    /* 渲染器 */
    const renderer = new WebGLRenderer()
    //renderer.physicallyCorrectLights = true
    renderer.setSize(dom.clientWidth, dom.clientHeight)
    dom.appendChild(renderer.domElement)
    /* 立方体 */
    const geometry = new BoxGeometry(1, 1, 1)
    //材质对象Material
    const material = new MeshLambertMaterial({
/*      emissive: 0xffffee,
      emissiveIntensity: 1,
      color: 0x000000*/
    })
    const cube = new Mesh(geometry, material)
    cube.rotation.x += 1
    cube.rotation.y += 1
    // 让立方体自发光
    const cubeLight = new PointLight(0xff0088, 0.5, 100, 2)
    cubeLight.add(cube)
    cubeLight.castShadow = true
    // 物体将会被添加到(0,0,0)坐标
    cubeLight.position.set(0, 0, 0)
    scene.add(cubeLight)
    /* 平行光 */
    const light = new DirectionalLight(0xff0000, 0.2)
    light.position.set(0, 10, 5)
    scene.add(light)
    /* 环境光 */
    const ambientLight = new AmbientLight()
    scene.add(ambientLight)
    /* 渲染循环 */
    const animate = () => {
      requestAnimationFrame(animate)
/*      cube.rotation.x += 0.01
      cube.rotation.y += 0.01*/
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