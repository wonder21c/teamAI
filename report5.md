### 재질 (Material) 1

#### meshBasicMaterial
```
import { OrbitControls } from "@react-three/drei";
import { useEffect, useRef } from "react";
import * as THREE from "three"

function MyElement3D() {
    const mesh1 = useRef()
    const mesh2 = useRef()

    useEffect(() => {
        mesh2.current.material = mesh1.current.material
    }, [])

    return (
        <>
            <OrbitControls />

            <ambientLight intensity = {0.2} />

            <directionalLight position = {[0, 1, 0]} />
            <directionalLight position = {[1, 2, 8]} intensity = {0.7} />

            <mesh 
                ref = {mesh1}
                position = {[0.7, 0, 0]}
            >
                <boxGeometry />

                {/* 
                visible : 보이는지 안보이는지 true/false
                transparent : 재질 투명 효과 true/false
                opacity : 투명도 (1 : 불투명, 0 : 투명) - transparent가 true일때만 작동
                depthTest : 렌더링 되고 있는 Mesh의 픽셀을 depthBuffer 값을 활용하여 검사할 것인지
                depthWrite : 렌더링 되고 있는 Mesh의 픽셀에 대한 Z 값을 depthBuffer에 기록할 것인지
                side : Mesh를 구성하고 있는 면 중, 어느 면을 렌더링 할 것인지 (기본값 : FrontSide)
                */}
                <meshBasicMaterial 
                    color = "yellow" 
                    wireframe = {false}
                    visible={true}
                    transparent = {true}
                    opacity = {0.5}
                    depthTest = {true}
                    depthWrite = {true}
                    side = {THREE.DoubleSide}
                />
            </mesh>

            <mesh 
                ref = {mesh2}
                position = {[-0.7, 0, 0]}
            >
                <torusGeometry args={[0.5, 0.2]} />
            </mesh>
        </>
    )
}

export default MyElement3D
```

#### meshLambertMaterial
```
import { OrbitControls } from "@react-three/drei";
import { useEffect, useRef } from "react";
import * as THREE from "three"

function MyElement3D() {
    const mesh1 = useRef()
    const mesh2 = useRef()

    useEffect(() => {
        mesh2.current.material = mesh1.current.material
    }, [])

    return (
        <>
            <OrbitControls />

            <ambientLight intensity = {0.2} />

            <directionalLight position = {[0, 1, 0]} />
            <directionalLight position = {[1, 2, 8]} intensity = {0.7} />

            <mesh 
                ref = {mesh1}
                position = {[0.7, 0, 0]}
            >
                <boxGeometry />

                {/* 
                visible : 보이는지 안보이는지 true/false
                transparent : 재질 투명 효과 true/false
                opacity : 투명도 (1 : 불투명, 0 : 투명) - transparent가 true일때만 작동
                depthTest : 렌더링 되고 있는 Mesh의 픽셀을 depthBuffer 값을 활용하여 검사할 것인지
                depthWrite : 렌더링 되고 있는 Mesh의 픽셀에 대한 Z 값을 depthBuffer에 기록할 것인지
                side : Mesh를 구성하고 있는 면 중, 어느 면을 렌더링 할 것인지 (기본값 : FrontSide)
                */}
                <meshLambertMaterial
                    color = "#d25383" 
                    wireframe = {false}
                    visible={true}
                    transparent = {true}
                    opacity = {1}
                    depthTest = {true}
                    depthWrite = {true}
                    side = {THREE.FrontSide}

                    // 재질 자체에서 검출하는 속성값 (기본 : 검정색 - 어떤 색상도 검출 X)
                    // 위 색이랑 섞임
                    emissive={0x666600}
                />
            </mesh>

            <mesh 
                ref = {mesh2}
                position = {[-0.7, 0, 0]}
            >
                <torusGeometry args={[0.5, 0.2]} />
            </mesh>
        </>
    )
}

export default MyElement3D
```

#### meshPhongMaterial

```
import { OrbitControls } from "@react-three/drei";
import { useEffect, useRef } from "react";
import * as THREE from "three"

function MyElement3D() {
    const mesh1 = useRef()
    const mesh2 = useRef()

    useEffect(() => {
        mesh2.current.material = mesh1.current.material
    }, [])

    return (
        <>
            <OrbitControls />

            <ambientLight intensity = {0.2} />

            <directionalLight position = {[0, 1, 0]} />
            <directionalLight position = {[1, 2, 8]} intensity = {0.7} />

            <mesh 
                ref = {mesh1}
                position = {[0.7, 0, 0]}
            >
                <boxGeometry />

                {/* 
                visible : 보이는지 안보이는지 true/false
                transparent : 재질 투명 효과 true/false
                opacity : 투명도 (1 : 불투명, 0 : 투명) - transparent가 true일때만 작동
                depthTest : 렌더링 되고 있는 Mesh의 픽셀을 depthBuffer 값을 활용하여 검사할 것인지
                depthWrite : 렌더링 되고 있는 Mesh의 픽셀에 대한 Z 값을 depthBuffer에 기록할 것인지
                side : Mesh를 구성하고 있는 면 중, 어느 면을 렌더링 할 것인지 (기본값 : FrontSide)
                emissive : 재질 자체에서 검출하는 속성값 (기본 : 검정색 - 어떤 색상도 검출 X)
                 color 색이랑 섞임
                */}
                <meshPhongMaterial
                    wireframe = {false}
                    visible={true}
                    transparent = {true}
                    opacity = {1}
                    depthTest = {true}
                    depthWrite = {true}
                    side = {THREE.FrontSide}

                    emissive = {0x666600}
                    color = {0xff0000} 

                    // specular : 광원에 의해 반사되는 색상 값
                    // shininess : specular의 반사 정도 조절
                    specular = {0xffff00}
                    shininess = {100}

                    // flatShading : mesh를 평평하게 렌더링할 지 여부
                    flatShading = {true}
                />
            </mesh>

            <mesh 
                ref = {mesh2}
                position = {[-0.7, 0, 0]}
            >
                <torusGeometry args={[0.5, 0.2]} />
            </mesh>
        </>
    )
}

export default MyElement3D
```

#### meshStandardMaterial
```
import { OrbitControls } from "@react-three/drei";
import { useControls } from "leva";
import { useEffect, useRef } from "react";
import * as THREE from "three"

function MyElement3D() {
    const mesh1 = useRef()
    const mesh2 = useRef()

    useEffect(() => {
        mesh2.current.material = mesh1.current.material
    }, [])

    const {roughness, metalness} = useControls({
        roughness: {value: 0, min: 0, max: 1, step: 0.01},
        metalness: {value: 0, min: 0, max: 1, step: 0.01}
    })

    return (
        <>
            <OrbitControls />

            <ambientLight intensity = {0.2} />

            <directionalLight position = {[0, 1, 0]} />
            <directionalLight position = {[1, 2, 8]} intensity = {0.7} />

            <mesh 
                ref = {mesh1}
                position = {[0.7, 0, 0]}
            >
                <boxGeometry />

                <meshStandardMaterial 
                    visible={true}
                    transparent = {true}
                    opacity = {0.5}
                    depthTest = {true}
                    depthWrite = {true}
                    side = {THREE.FrontSide}

                    emissive = {0x00000}
                    flatShading = {false}

                    color = {0xff0000} 
                    wireframe = {false}

                    // meshStandardMaterial 고유 특성
                    roughness = {roughness}
                    metalness = {metalness}
                />
            </mesh>

            <mesh 
                ref = {mesh2}
                position = {[-0.7, 0, 0]}
            >
                <torusGeometry args={[0.5, 0.2]} />
            </mesh>
        </>
    )
}

export default MyElement3D
```

### meshPhysicalMaterial
```
import { OrbitControls } from "@react-three/drei";
import { useEffect, useRef } from "react";
import { useControls } from "leva";
import * as THREE from "three"

function MyElement3D() {
    const mesh1 = useRef()
    const mesh2 = useRef()

    useEffect(() => {
        mesh2.current.material = mesh1.current.material
    }, [])

    const {roughness, metalness, clearcoat, clearcoatRoughness, transmission, thickness, ior} = useControls({
        roughness: {value: 0, min: 0, max: 1, step: 0.01},
        metalness: {value: 0, min: 0, max: 1, step: 0.01},
        clearcoat: {value: 0, min: 0, max: 1, step: 0.01}, 
        clearcoatRoughness: {value: 0, min: 0, max: 1, step: 0.01},
        transmission: {value: 0, min: 0, max: 1, step: 0.01},
        thickness: {value: 0, min: 0, max: 1, step: 0.01},
        ior: {value: 1.5, min: 0, max: 2.333, step: 0.01}
    })

    return (
        <>
            <OrbitControls />

            <ambientLight intensity = {0.2} />

            <directionalLight position = {[0, 1, 0]} />
            <directionalLight position = {[1, 2, 8]} intensity = {0.7} />

            <mesh 
                ref = {mesh1}
                position = {[0.7, 0, 0]}
            >
                <torusKnotGeometry args = {[0.5, 0.15, 256, 128]} />
              
                <meshPhysicalMaterial 
                    visible={true}
                    transparent = {true}
                    opacity = {0.5}
                    depthTest = {true}
                    depthWrite = {true}
                    side = {THREE.DoubleSide}
                    emissive = {0x00000}
                    flatShading = {false}
                    roughness = {roughness}
                    metalness = {metalness}

                    color = {0xffffff} 
                    wireframe = {false}

                    // meshPhysicalMaterial 고유 속성
                    // clearcoat : 코팅된 광택 있는 층
                    // clearcoatRoughness :  clearcoat 표면의 거칠기
                    clearcoat = {clearcoat}
                    clearcoatRoughness = {clearcoatRoughness}

                    // meshPhysicalMaterial 유리에 사용되는 고유 속성
                    // transmission : 유리투명도
                    // thickness : 유리 두께
                    // ior : 유리 굴절률
                    transmission = {transmission}
                    thickness = {thickness}
                    ior = {ior}
                />
            </mesh>

            <mesh 
                ref = {mesh2}
                position = {[-0.7, 0, 0]}
            >
                <torusGeometry args={[0.5, 0.2]} />
            </mesh>
        </>
    )
}

export default MyElement3D
```

#### meshDepthMaterial
```
import { OrbitControls } from "@react-three/drei";
import { useEffect, useRef } from "react";
import { useControls } from "leva";
import * as THREE from "three"

function MyElement3D() {
    const mesh1 = useRef()
    const mesh2 = useRef()

    useEffect(() => {
        mesh2.current.material = mesh1.current.material
    }, [])

    const {roughness, metalness, clearcoat, clearcoatRoughness, transmission, thickness, ior} = useControls({
        roughness: {value: 0, min: 0, max: 1, step: 0.01},
        metalness: {value: 0, min: 0, max: 1, step: 0.01},
        clearcoat: {value: 0, min: 0, max: 1, step: 0.01}, 
        clearcoatRoughness: {value: 0, min: 0, max: 1, step: 0.01},
        transmission: {value: 0, min: 0, max: 1, step: 0.01},
        thickness: {value: 0, min: 0, max: 1, step: 0.01},
        ior: {value: 1.5, min: 0, max: 2.333, step: 0.01}
    })

    return (
        <>
            <OrbitControls />

            <ambientLight intensity = {0.2} />

            <directionalLight position = {[0, 1, 0]} />
            <directionalLight position = {[1, 2, 8]} intensity = {0.7} />

            <mesh 
                ref = {mesh1}
                position = {[0.7, 0, 0]}
            >
                <torusKnotGeometry args = {[0.5, 0.15, 256, 128]} />
              
                <meshDepthMaterial />
            </mesh>

            <mesh 
                ref = {mesh2}
                position = {[-0.7, 0, 0]}
            >
                <torusGeometry args={[0.5, 0.2]} />
            </mesh>
        </>
    )
}

export default MyElement3D
```
#### App.jsx
```
import './App.css'
import { Canvas } from '@react-three/fiber'
import MyElement3D from './Component/MyElement3D'

function App() {
  return (
    <>
      {/* camera로부터 거리가 3.5인 픽셀지점은 그 값을 0으로 할당, 
          camera로부터 거리가 6인 지점은 2를 할당 */}
      <Canvas camera = {{near: 3.5, far: 6}} >
        <MyElement3D/>
      </Canvas>   
    </>
  )
}

export default App
```

#### meshMatcapMaterial
```
import { OrbitControls, useTexture } from "@react-three/drei";
import { useEffect, useRef } from "react";
import { useControls } from "leva";
import * as THREE from "three"

function MyElement3D() {
    const mesh1 = useRef()
    const mesh2 = useRef()

    useEffect(() => {
        mesh2.current.material = mesh1.current.material
    }, [])

    // matcap 이미지 불러오기
    const matcap = useTexture("././public/images/matcap.jpg")

    return (
        <>
            <OrbitControls />

            <ambientLight intensity = {0.2} />

            {/* meshMatcapMaterial은 광원을 필요로 하지 않는다. */}
            {/* <directionalLight position = {[0, 1, 0]} />
            <directionalLight position = {[1, 2, 8]} intensity = {0.7} /> */}

            <mesh 
                ref = {mesh1}
                position = {[0.7, 0, 0]}
            >
                <torusKnotGeometry args = {[0.5, 0.15, 256, 128]} />

                {/* <meshDepthMaterial/> */}
                {/* flatShading : 각진 면으로 표현 */}
                <meshMatcapMaterial matcap={matcap} 
                    flatShading = {true}
                />
                
            </mesh>

            <mesh 
                ref = {mesh2}
                position = {[-0.7, 0, 0]}
            >
                <torusGeometry args={[0.5, 0.2]} />
            </mesh>
        </>
    )
}

export default MyElement3D
```

#### meshToonMaterial
```
import { OrbitControls, useTexture } from "@react-three/drei";
import { useEffect, useRef } from "react";
import { useControls } from "leva";
import * as THREE from "three"

function MyElement3D() {
    const mesh1 = useRef()
    const mesh2 = useRef()

    useEffect(() => {
        mesh2.current.material = mesh1.current.material
    }, [])

    // tone 불러오기
    const texture = useTexture("././public/images/threeTone.jpg")
    // 색상 보관이 이루어지지 않도록 함. 
    texture.minFilter = THREE.NearestFilter
    texture.magFilter = THREE.NearestFilter

    return (
        <>
            <OrbitControls />

            <ambientLight intensity = {0.2} />

            {/* meshMatcapMaterial은 광원을 필요로 하지 않는다. */}
            {/* <directionalLight position = {[0, 1, 0]} />
            <directionalLight position = {[1, 2, 8]} intensity = {0.7} /> */}

            <mesh 
                ref = {mesh1}
                position = {[0.7, 0, 0]}
            >
                <torusKnotGeometry args = {[0.5, 0.15, 256, 128]} />

                <meshToonMaterial gradientMap={texture} color="cyan" />
                
            </mesh>

            <mesh 
                ref = {mesh2}
                position = {[-0.7, 0, 0]}
            >
                <torusGeometry args={[0.5, 0.2]} />
            </mesh>
        </>
    )
}

export default MyElement3D
```
