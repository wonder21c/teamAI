### 카메라 (Camera)
![chrome-capture-2024-5-19](https://github.com/wonder21c/teamAI/assets/50861700/3df7ac6f-f8e9-4f2d-82cc-6141586e9c6a)

#### Perspective Camera 

#### App.jsx
```
import './App.css'
import { Canvas } from '@react-three/fiber'
import MyElement3D from './Component/MyElement3D'

function App() {
  return (
    <>
      {/* 기본 카메라 : Perspective Camera */}
      {/* 카메라 렌즈 화각 : 75도
          카메라 위치 : 7, 7, 0 
      
      
      */}
      <Canvas camera = {{
        fov: 130,
        position: [7, 7, 0],
        near: 0.1,
        far: 20
      }} >
        <MyElement3D/>
      </Canvas>   
    </>
  )
}

export default App
```

#### MyElement3D.jsx
```
import { Environment, OrbitControls, useHelper } from "@react-three/drei";
import { useFrame, useThree } from "@react-three/fiber";
import { useEffect, useRef } from "react";
import * as THREE from "three"
import {RectAreaLightUniformsLib} from "three/examples/jsm/lights/RectAreaLightUniformsLib"
import {RectAreaLightHelper} from "three/examples/jsm/helpers/RectAreaLightHelper"

RectAreaLightUniformsLib.init()

const torusGeometry = new THREE.TorusGeometry(0.4, 0.1, 32, 32)
const torusMaterial = new THREE.MeshStandardMaterial({
    color: "#9b59b6",
    roughness: 0.5,
    metalness: 0.9
})

function MyElement3D() {
    useFrame((state) => {
        const time = state.clock.elapsedTime
        const smallSpherePivot = state.scene.getObjectByName("smallSpherePivot")

        smallSpherePivot.rotation.y = THREE.MathUtils.degToRad(time * 50)

        const target = new THREE.Vector3()
        smallSpherePivot.children[0].getWorldPosition(target)
        state.camera.position.copy(target)
        
        const ghostSpherePivot = state.scene.getObjectByName("ghostSpherePivot")
        ghostSpherePivot.rotation.y = THREE.MathUtils.degToRad(time * 50 + 30)
        ghostSpherePivot.children[0].getWorldPosition(target)
        state.camera.lookAt(target)
    })

    const light = useRef()
    useHelper(light, RectAreaLightHelper)

    // 카메라 객체 가져오기
    const {camera} = useThree()
    // useControls({
    //     positionZ: {
    //         value: 0, min: -10, max: 10, step: 0.1,
    //         onchange: (v) => camera.position.z = v
    //     },
    //     targetZ: {
    //         value: 0, min: -10, max: 10, step: 0.1,
    //         onchange: (v) => camera.lookAt(0, 0, v)
    //     }
    // })

    return (
        <>
            {/* <OrbitControls /> */}

            <rectAreaLight 
                color={"#ffffff"}
                intensity={20}
                width={1}
                height={3}

                ref={light}
                position={[0, 5, 0]}
                rotation-x={THREE.MathUtils.degToRad(-90)}
            />

            <mesh rotation-x={THREE.MathUtils.degToRad(-90)}>
                <sphereGeometry args={[1.5, 64, 64, 0, Math.PI]} />

                <meshStandardMaterial 
                    color={"#ffffff"}
                    roughness={0.1}
                    metalness={0.5}
                />
            </mesh>

            <mesh rotation-x={THREE.MathUtils.degToRad(-90)}>
                <sphereGeometry args={[1.5, 64, 64, 0, Math.PI]} />
                <meshStandardMaterial 
                    color={"#ffffff"}
                    roughness={0.1}
                    metalness={0.2}
                />
            </mesh>

            {new Array(10).fill().map((item, index) => {
                return (
                    <group key={index} rotation-y={THREE.MathUtils.degToRad(45 * index)}>
                        <mesh 
                            geometry={torusGeometry}
                            material={torusMaterial}
                            position={[3, 0.5, 0]}
                        />
                    </group>
                )
            })}

            <axesHelper />

            <group name="smallSpherePivot">
                <mesh position={[3, 0.5, 0]}>
                    <sphereGeometry args={[0.3, 32, 32]} />

                    <meshStandardMaterial 
                        color={"e74c3c"}
                        roughness={0.2}
                        metalness={0.5}
                    />
                </mesh>
            </group>

            <group name="ghostSpherePivot">
                <object3D position={[3, 0.5, 0]} />
            </group>
        </>
    )
}

export default MyElement3D
```

#### Orthographic Camera

#### App.jsx
```
import './App.css'
import { Canvas } from '@react-three/fiber'
import MyElement3D from './Component/MyElement3D'

function App() {
  return (
    <>
      {/* 기본 카메라 : Perspective Camera */}
      {/* 카메라 렌즈 화각 : 75도
          카메라 위치 : 7, 7, 0 
      
      
      */}
      <Canvas 
        orthographic
        camera = {{
          near: 0.1,
          far: 20,
          position: [7, 7, 0],
          zoom: 100
      }} >
        <MyElement3D/>
      </Canvas>   
    </>
  )
}

export default App

```


