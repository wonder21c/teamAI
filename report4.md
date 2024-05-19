### 지오메트리 (Geometry) 2

#### 실행화면

![image](https://github.com/qkrgudals1030/teamAI/assets/50895124/5dcc4412-9de5-44a0-9001-225785ede17c)

![image](https://github.com/qkrgudals1030/teamAI/assets/50895124/d17ab137-0414-48e3-a416-8caeed99d972)


#### SphereGeometry의 args 속성
```
import { OrbitControls, Box } from "@react-three/drei";
import { useControls } from "leva";
import { useEffect, useRef } from "react";

function MyElement3D() {

    const refMesh = useRef()
    const refWireMesh = useRef()

    const { radius, widthSegments, heightSegments, phiStart, phiLength, thetaStart, thetaLength } = useControls({
        radius: { value: 1, min: 0.1, max: 5, step: 0.01 },
        
        // 아래 두 값은 정수이어야 한다.
        widthSegments: { value: 32, min: 3, max: 256, step: 1 },
        heightSegments: { value: 1, min: 3, max: 256, step: 1 },

        phiStart: { value: 0, min: 0, max: 360, step: 0.1 },
        phiLength: { value: 360, min: 0, max: 360, step: 0.1 },
        
        thetaStart: { value: 0, min: 0, max: 180, step: 0.1 },
        thetaLength: { value: 180, min: 0, max: 180, step: 0.1 }
    })
 
    useEffect(() => {
        refWireMesh.current.geometry = refMesh.current.geometry
        }, [radius, widthSegments, heightSegments, phiStart, phiLength])

    return (
        <>
            <OrbitControls />

            <ambientLight intensity = {0.1} />

            <directionalLight 
                position = {[2, 1, 3]}
                intensity = {0.5}
            />
                  
            <mesh ref={refMesh}>
                <sphereGeometry args={[
                    radius, 
                    widthSegments, heightSegments, 
                    phiStart * Math.PI/180, phiLength * Math.PI/180,
                    thetaStart * Math.PI/180, thetaLength * Math.PI/180
                ]} />

                <meshStandardMaterial color="#1abc9c" />
            </mesh>

            <mesh ref={refWireMesh}>
                <meshStandardMaterial 
                    emissive = "yellow" 
                    wireframe={true}
                />
            </mesh>

            <axesHelper scale={10} />
        </>
    )
}

export default MyElement3D
```

#### CylinderGeometry의 args 속성
```
import { OrbitControls, Box } from "@react-three/drei";
import { useControls } from "leva";
import { useEffect, useRef } from "react";

function MyElement3D() {

    const refMesh = useRef()
    const refWireMesh = useRef()

    const { topRadius, bottomRadius, height, radialSegments, heightSegments, bopen, thetaStart, thetaLength } = useControls({
        
        topRadius: { value: 1, min: 0.1, max: 5, step: 0.01 },
        bottomRadius: { value: 1, min: 0.1, max: 5, step: 0.01 },
        
        height: { value: 1, min: 0.1, max: 5, step: 0.01 },

        radialSegments: { value: 32, min: 1, max: 256, step: 1},
        heightSegments: { value: 1, min: 1, max: 256, step: 1 },
        bopen: { value: false},

        thetaStart: { value: 0, min: 0, max: 360, step: 0.01 },
        thetaLength: { value: 0, min: 0, max: 360, step: 0.01 }
    })
 
    useEffect(() => {

        refWireMesh.current.geometry = refMesh.current.geometry
    }, [topRadius, bottomRadius, height, radialSegments, heightSegments, bopen, thetaStart, thetaLength])

    return (
        <>
            <OrbitControls />

            <ambientLight intensity = {0.1} />

            <directionalLight 
                position = {[2, 1, 3]}
                intensity = {0.5}
            />

            <mesh ref={refMesh}>

                <cylinderGeometry args = {[
                    topRadius, bottomRadius,
                    height,
                    radialSegments, heightSegments,
                    bopen,
                    thetaStart * Math.PI/180, thetaLength * Math.PI/180
                ]} />

                <meshStandardMaterial color="#1abc9c" />
            </mesh>

            <mesh ref={refWireMesh}>

                <meshStandardMaterial 
                    emissive = "yellow" 
                    wireframe={true}
                />
            </mesh>

            <axesHelper scale={10} />
        </>
    )
}

export default MyElement3D
```




