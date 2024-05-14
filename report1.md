### 3차원 정육면체 모델 생성, 색상 정의, 조명 설치

### 손정우 테스트

#### App.jsx

```
import './App.css'
import { Canvas } from '@react-three/fiber'
import MyElement3D from './MyElement3D'

function App() {
  return (
    <>
      	<Canvas>
            // 컴포넌트 호출
          	<MyElement3D />
      	</Canvas>
    </>
  )
}

export default App
```
#### MyElement3D.jsx (컴포넌트)
```
function MyElement3D {
 	return (
    	<>
        	// 조명 설정
        	<directionalLight position={[1, 1, 1]} />
        
        	// mesh : 3차원 모델
        	<mesh>
              // boxGeometry : 정육면체
              <boxGeometry />
              
              // mesh의 색상을 정의하기 위해 material 설정
              <meshStandardMaterial color="#e67e22" />
        	</mesh>
        </>
    )
}

export default MyElement3D

```

#### MyElement3D.jsx
```
import { useRef } from "react"
import { useFrame } from "@react-three/fiber"

function MyElement3D {
  	// useRef 훅
    const refMesh = useRef()
  
    // delta : 이전 프레임과 현재 프레임 사이의 경과 시간 (단위 : 밀리초)
    useFrame((state, delta) => {
    	// 콜백함수 : 매 프레임이 렌더링 되기 전 호출되는 함수
      // 매 프레임마다 delta씩 회전 => 무한 회전
      refMesh.current.rotation.y += delta
    })
    
 	return (
    	<>
        	<directionalLight position={[1, 1, 1]} />
        
        	// y축 90도 방향 회전
        	<mesh ref={refMesh} rotation-y={[45*Math.PI/180]}>
              <boxGeometry />
              
              <meshStandardMaterial color="#e67e22" />
        	</mesh>
        </>
    )
}

export default MyElement3D
```


