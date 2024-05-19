### 지오메트리 (Geometry) 1
![geometry-2024-4-30](https://github.com/wonder21c/computer-graphic/assets/50861700/c4bb02ab-743b-4db6-b58e-af0569f0ff87)


#### 같은 객체를 표현하는 세 가지 방법
```
import { OrbitControls, Box } from "@react-three/drei";
import * as THREE from "three"

function MyBox(props) {
    const geom = new THREE.BoxGeometry()

    return (
        <mesh
            {...props}
            geometry={geom}
        >
        
        </mesh>
    )
}

function MyElement3D() {

    return (
        <>
            <OrbitControls />

            <ambientLight intensity = {0.1} />

            <directionalLight 
                position = {[2, 1, 3]}
                intensity = {0.5}
            />

            {/* 동일한 Box Geometry를 표현하는 3가지 방법 */}


            {/* 방법 1. mesh */}
            <mesh>
                <boxGeometry />

                <meshStandardMaterial color = "#1abc9c" />
            </mesh>

            {/* 방법 2. Drei 라이브러리의 box */}
            <Box position={[1.2, 0, 0]}>
                <meshStandardMaterial color={"#8e44ad"} />
            </Box>

            {/* 방법 3. 커스텀 함수를 통해 생성 */}
            <MyBox position={[-1.2, 0, 0]}>
                <meshStandardMaterial color="#e74c3c" />
            </MyBox>
        </>
    )
}

export default MyElement3D
```

#### 하나의 boxGeometry로 두 Mesh를 표현

```
import { OrbitControls, Box } from "@react-three/drei";
import { useEffect, useRef } from "react";
import * as THREE from "three"

function MyElement3D() {

    const refMesh = useRef()
    const refWireMesh = useRef()

	useEffect(() => {
        refWireMesh.current.geometry = refMesh.current.geometry
    }, [])
    
    return (
        <>
            <OrbitControls />

            <ambientLight intensity = {0.1} />

            <directionalLight 
                position = {[2, 1, 3]}
                intensity = {0.5}
            />


            {/* 위에서 UseEffect를 활용하여 하나의 boxGeometry만 사용하고도 두 Mesh 모두 표현 */}
            <mesh ref={refMesh}>
                <boxGeometry />

                <meshStandardMaterial color="#1abc9c" />
            </mesh>

            <mesh ref={refWireMesh}>
                {/* <boxGeometry /> */}

                <meshStandardMaterial 
                    emissive = "yellow" 
                    wireframe={true}
                />
            </mesh>
        </>
    )
}

export default MyElement3D
```


####  코드를 사용하지 않고 UI로 크기를 변경시켜보기
```
import { OrbitControls, Box } from "@react-three/drei";
import { useEffect, useRef } from "react";
import * as THREE from "three"

function MyElement3D() {

    const refMesh = useRef()
    const refWireMesh = useRef()

    useEffect(() => {
        refWireMesh.current.geometry = refMesh.current.geometry
    }, [])

    return (
        <>
            <OrbitControls />

            <ambientLight intensity = {0.1} />

            <directionalLight 
                position = {[2, 1, 3]}
                intensity = {0.5}
            />
        
            <mesh ref={refMesh}>
                {/* boxGeometry는 args를 활용해서 6개의 값을 지정할 수 있음 */}
                {/* 직접 지정하지 않으면 기본 값이 들어간다 (1) */}
                <boxGeometry args={[2, 1, 4, 1, 1, 1]} />

                <meshStandardMaterial color="#1abc9c" />
            </mesh>

            <mesh ref={refWireMesh}>

                <meshStandardMaterial 
                    emissive = "yellow" 
                    wireframe={true}
                />
            </mesh>
        </>
    )
}

export default MyElement3D
```

#### leva 라이브러리를 활용해야 한다.

```
import { OrbitControls, Box } from "@react-three/drei";
import { useControls } from "leva";
import { useEffect, useRef } from "react";

function MyElement3D() {

    const refMesh = useRef()
    const refWireMesh = useRef()

    const { xSize, ySize, zSize, xSegments, ySegments, zSegments } = useControls({
        // 초기값 : 1
        // 0.1과 5 사이의 값을 가진다.
        // UI를 활용한 조정 단위 : 0.1
        xSize: { value: 1, min: 0.1, max: 5, step: 0.01 },
        ySize: { value: 1, min: 0.1, max: 5, step: 0.01 },
        zSize: { value: 1, min: 0.1, max: 5, step: 0.01 },

        // Segment는 1보다 큰 정수여야 한다.
        xSegments: { value: 1, min: 1, max: 10, step: 1 },
        ySegments: { value: 1, min: 1, max: 10, step: 1 },
        zSegments: { value: 1, min: 1, max: 10, step: 1 }
    })
 
    useEffect(() => {
        refWireMesh.current.geometry = refMesh.current.geometry
    }, [xSize, ySize, zSize, xSegments, ySegments, zSegments])

    return (
        <>
            <OrbitControls />

            <ambientLight intensity = {0.1} />

            <directionalLight 
                position = {[2, 1, 3]}
                intensity = {0.5}
            />
        
            <mesh ref={refMesh}>
              
            <boxGeometry args={[xSize, ySize, zSize, xSegments, ySegments, zSegments]} />

                <meshStandardMaterial color="#1abc9c" />
            </mesh>

            <mesh ref={refWireMesh}>

                <meshStandardMaterial 
                    emissive = "yellow" 
                    wireframe={true}
                />
            </mesh>
        </>
    )
}

export default MyElement3D

```
