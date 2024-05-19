### 실행화면

![project](https://github.com/qkrgudals1030/teamAI/assets/50895124/66b499a0-cf81-4e27-80ca-01cdff3533d7)


#### css파일
```
body {
    margin: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    height: 100vh;
    justify-content: center;
    background-color: black;
    overflow: hidden;
}

.image-container {
    width: 200px;
    height: 200px;
    transform-style: preserve-3d;
    transform: perspective(1000px) rotateY(0deg);
    transition: transform .7s;
}

.image-container span {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    transform: rotateY(calc(var(--i) * 90deg)) translateZ(400px);
}

.image-container span img {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
  aspect-ratio: 1/1;
  -o-object-fit: cover;
     object-fit: cover;
  filter: grayscale(100%);

}

.btn-container {
    position: relative;
    width: 80%;
}

.btn {
  position: absolute;
  bottom: -140px;
  background-color: slateblue;
  color: white;
  border: none;
  padding: 10px 30px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 20px;
}


.btn:hover {
    filter: brightness(1.5);
}

.image-container span img:hover {
  filter: none;
}

#prev {
    left: 20%;
}

#next {
    right: 20%;
}
```

#### html
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Image Carousel with Reflection</title>
    <style>
        body {
            margin: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            background: linear-gradient(135deg, #2b2b2b, #1a1a1a);
            overflow: hidden;
            color: white;
            font-family: 'Arial', sans-serif;
        }

        .carousel-container {
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .image-container {
            width: 300px;
            height: 300px;
            position: relative;
            transform-style: preserve-3d;
            transform: perspective(1000px) rotateY(0deg);
            transition: transform 0.7s ease-in-out;
        }

        .image-container span {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            transform: rotateY(calc(var(--i) * 90deg)) translateZ(150px);
            backface-visibility: hidden;
        }

        .image-container span img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            border-radius: 10px;
            box-shadow: 0 10px 20px rgba(255, 255, 255, 0.3), 0 0 20px rgba(255, 255, 255, 0.2);
            transition: transform 0.3s, filter 0.3s, box-shadow 0.3s;
            filter: grayscale(100%) brightness(0.9);
        }

        .image-container span img:hover {
            transform: scale(1.1);
            filter: grayscale(0%) brightness(1);
            box-shadow: 0 10px 20px rgba(255, 255, 255, 0.8), 0 0 30px rgba(255, 255, 255, 0.6);
        }

        .reflection-container {
            position: absolute;
            top: 100%;
            left: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            pointer-events: none;
        }

        .reflection {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 100%;
            transform: scaleY(-1);
            opacity: 0.4;
            filter: blur(5px);
        }

        .btn-container {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            width: 70%;
            display: flex;
            justify-content: space-between;

        }

        .btn {
            background-color: slateblue;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 20px;
            transition: background-color 0.3s, transform 0.3s;
        }

        .btn:hover {
            background-color: darkslateblue;
            transform: scale(1.1);
        }

        #prev {
            margin-right: auto;
        }

        #next {
            margin-left: auto;
        }
    </style>
</head>
<body>
    <div class="carousel-container">
        <div class="image-container">
            <span style="--i: 0">
                <img src="https://ssl.pstatic.net/static/nid/account/naver_og_image.png" class="clickable" data-url="https://www.naver.com">
                <div class="reflection-container">
                    <img src="https://ssl.pstatic.net/static/nid/account/naver_og_image.png" class="reflection" alt="Reflection">
                </div>
            </span>
            <span style="--i: 1">
                <img src="https://blog.google/static/blogv2/images/google-1000x1000.png" class="clickable" data-url="https://www.google.com">
                <div class="reflection-container">
                    <img src="https://blog.google/static/blogv2/images/google-1000x1000.png" class="reflection" alt="Reflection">
                </div>
            </span>
            <span style="--i: 2">
                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/ae/Github-desktop-logo-symbol.svg/2048px-Github-desktop-logo-symbol.svg.png" class="clickable" data-url="https://github.com/qkrgudals1030/teamAI">
                <div class="reflection-container">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/ae/Github-desktop-logo-symbol.svg/2048px-Github-desktop-logo-symbol.svg.png" class="reflection" alt="Reflection">
                </div>
            </span>
            <span style="--i: 3">
                <img src="https://www.youtube.com/img/desktop/yt_1200.png" class="clickable" data-url="https://www.youtube.com">
                <div class="reflection-container">
                    <img src="https://www.youtube.com/img/desktop/yt_1200.png" class="reflection" alt="Reflection">
                </div>
            </span>
        </div>
        <div class="btn-container">
            <button class="btn" id="prev">&larr; Prev</button>
            <button class="btn" id="next">Next &rarr;</button>
        </div>
    </div>

    <script>
        const imageContainerEl = document.querySelector(".image-container");
        const prevEl = document.getElementById("prev");
        const nextEl = document.getElementById("next");
        const clickableEls = document.querySelectorAll(".clickable");

        let x = 0;
        let timer;

        prevEl.addEventListener("click", () => {
            x += 90;
            clearTimeout(timer);
            updateGallery();
        });

        nextEl.addEventListener("click", () => {
            x -= 90;
            clearTimeout(timer);
            updateGallery();
        });

        clickableEls.forEach(el => {
            el.addEventListener("click", () => {
                const url = el.getAttribute("data-url");
                window.open(url, '_blank');
            });
        });

        function updateGallery() {
            imageContainerEl.style.transform = `perspective(1000px) rotateY(${x}deg)`;
            timer = setTimeout(() => {
                x -= 90;
                updateGallery();
            }, 3000);
        }

        updateGallery();
    </script>
</body>
</html>
```

#### js
```
const imageContainerEl = document.querySelector(".image-container");
const prevEl = document.getElementById("prev");
const nextEl = document.getElementById("next");
const clickableEls = document.querySelectorAll(".clickable");

let x = 0;
let timer;

prevEl.addEventListener("click", () => {
    x += 90;
    clearTimeout(timer);
    updateGallery();
});

nextEl.addEventListener("click", () => {
    x -= 90;
    clearTimeout(timer);
    updateGallery();
});

function updateGallery() {
    imageContainerEl.style.transform = `perspective(1000px) rotateY(${x}deg)`;
    timer = setTimeout( () => {
        x -= 90;
        updateGallery();
    }, 3000)
}
updateGallery();
```

