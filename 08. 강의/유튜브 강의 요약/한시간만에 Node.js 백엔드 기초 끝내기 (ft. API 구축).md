# [한시간만에 Node.js 백엔드 기초 끝내기 (ft. API 구축)](https://www.youtube.com/watch?v=Tt_tKhhhJqY)

이 영상에서는 Node.js를 소개하고 사용하는 방법을 다룹니다. Node.js는 JavaScript를 서버에서 실행할 수 있게 해주는 환경으로, 백엔드 개발에 적합하며 널리 사용됩니다. Node.js의 주요 장점은 JavaScript를 서버 측에서 사용할 수 있게 하여, 프론트엔드와 백엔드에서 동일한 언어를 사용할 수 있도록 해주는 것입니다. 이를 통해 개발자가 동일한 기술 스택을 사용하여 전체 웹 애플리케이션을 개발할 수 있어, 학습 곡선이 줄어들고 개발 생산성이 높아집니다.

강사는 먼저 Node.js의 설치 방법을 설명하고, 이를 통해 JavaScript 코드를 로컬 환경에서 실행하는 방법을 보여줍니다. Node.js는 공식 웹사이트에서 설치할 수 있으며, 설치 후 명령줄에서 'node' 명령어를 사용하여 JavaScript 코드를 실행할 수 있습니다. 또한, Node 패키지 매니저(npm)에 대해서도 다룹니다. npm은 Node.js와 함께 설치되는 도구로, 수많은 오픈소스 라이브러리를 손쉽게 설치하고 관리할 수 있게 해줍니다. 이를 통해 필요한 기능을 빠르게 추가하고 개발 시간을 단축할 수 있습니다.

영상에서는 npm을 사용하여 Figlet과 Express 같은 모듈을 설치하는 방법을 시연합니다. Figlet은 텍스트를 ASCII 아트로 변환해주는 모듈이며, 간단한 예제로 사용됩니다. 이후 Express 모듈을 사용하여 간단한 웹 서버를 구축하는 과정을 설명합니다. Express는 Node.js에서 가장 널리 사용되는 웹 프레임워크 중 하나로, 간단하고 직관적인 방법으로 HTTP 요청을 처리하고 라우팅을 설정할 수 있게 해줍니다.

Express를 사용하여 특정 경로에 대한 요청을 처리하는 API를 만드는 과정도 다룹니다. 여기서 라우팅의 개념과 GET 요청을 처리하는 방법을 배우게 됩니다. 라우팅이란 클라이언트의 요청 경로에 따라 서버가 서로 다른 응답을 제공하는 것을 의미합니다. 예를 들어, `/sound/dog`과 같은 경로로 요청이 들어오면, 서버는 강아지의 울음소리인 "멍멍"을 반환하도록 구현합니다. 경로 매개변수를 사용해 요청에 따라 동물 소리를 다르게 반환하는 예제를 통해, 라우팅과 매개변수 처리에 대한 실습도 진행됩니다.

라우팅과 GET 요청을 처리하기 위해 Express에서 제공하는 `app.get()` 메서드를 사용합니다. 이 메서드는 특정 경로로 들어오는 GET 요청에 대해 응답을 설정하는 역할을 합니다. 예를 들어:

```javascript
const express = require("express"); // Express 모듈을 가져옵니다.
const app = express(); // Express 애플리케이션을 생성합니다.
const port = 3000; // 서버가 들을 포트를 설정합니다.

// 특정 경로에 대한 GET 요청을 처리하는 라우트 설정
app.get("/sound/:animal", (req, res) => {
  const { animal } = req.params; // 경로 매개변수에서 animal 값을 추출합니다.

  // 동물 소리에 따라 다른 응답을 설정합니다.
  if (animal === "dog") {
    res.json({ sound: "멍멍" });
  } else if (animal === "cat") {
    res.json({ sound: "야옹" });
  } else if (animal === "pig") {
    res.json({ sound: "꿀꿀" });
  } else {
    res.json({ sound: "알 수 없음" });
  }
});

// 서버를 설정한 포트에서 시작합니다.
app.listen(port, () => {
  console.log(`서버가 http://localhost:${port} 에서 실행 중입니다.`);
});
```

위 코드에서 `app.get()` 메서드는 `/sound/:animal` 경로로 들어오는 요청을 처리합니다. `:animal`은 경로 매개변수로, 요청 시 지정된 동물 이름에 따라 서로 다른 소리를 응답으로 제공합니다. 이 방식으로 다양한 라우팅을 설정하고 요청에 대한 처리를 쉽게 구현할 수 있습니다.

또한, 영상에서는 외부 요청을 허용하기 위해 CORS(Cross-Origin Resource Sharing) 설정을 추가하는 방법도 설명합니다. CORS는 보안상의 이유로 기본적으로 다른 출처에서 온 요청을 차단하는데, 이를 허용해야 할 경우 CORS 모듈을 사용하여 설정하는 방법을 배웁니다. 예를 들어, 다음과 같이 CORS 모듈을 설치하고 사용하는 방식으로 외부에서의 요청을 허용할 수 있습니다:

```bash
npm install cors
```

```javascript
const cors = require("cors"); // CORS 모듈을 가져옵니다.
app.use(cors()); // 모든 출처에서의 요청을 허용합니다.
```

이 설정을 통해 다른 도메인이나 포트에서 온 요청도 허용할 수 있게 되며, 이를 통해 프론트엔드와 백엔드 간의 데이터 통신이 원활해집니다. 이를 통해 개발자는 다른 출처에서의 요청도 처리할 수 있는 유연한 백엔드 서버를 구축할 수 있습니다.

마지막으로, 프론트엔드 HTML 페이지와 백엔드 API를 연동하는 과정을 시연합니다. HTML 페이지에서 버튼을 클릭하면 JavaScript의 `fetch` 함수를 사용하여 백엔드의 API에 요청을 보내고, 그 결과를 화면에 표시하는 방식입니다. 이를 통해 풀스택 애플리케이션의 기본적인 구조를 이해할 수 있으며, 백엔드에서 데이터를 처리하고 이를 프론트엔드에 전달하는 과정이 어떻게 이루어지는지를 배울 수 있습니다.

예를 들어, 다음과 같은 HTML과 JavaScript 코드가 있다고 가정해 봅시다:

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>동물 소리 가져오기</title>
  </head>
  <body>
    <h1>동물 소리 가져오기</h1>
    <input type="text" id="animalInput" placeholder="동물 이름을 입력하세요 (예: dog, cat, pig)" />
    <button onclick="getAnimalSound()">소리 가져오기</button>
    <h2 id="result"></h2>

    <script>
      function getAnimalSound() {
        const animal = document.getElementById("animalInput").value; // 입력한 동물 이름을 가져옵니다.

        // 백엔드 API에 GET 요청을 보냅니다.
        fetch(`http://localhost:3000/sound/${animal}`)
          .then((response) => response.json()) // 응답을 JSON 형태로 변환합니다.
          .then((data) => {
            document.getElementById("result").innerText = `소리: ${data.sound}`; // 응답 데이터를 화면에 표시합니다.
          })
          .catch((error) => {
            console.error("오류 발생:", error); // 오류가 발생하면 콘솔에 출력합니다.
          });
      }
    </script>
  </body>
</html>
```

위의 코드에서 사용자는 입력 필드에 동물 이름을 입력하고 버튼을 클릭하여 해당 동물의 소리를 가져올 수 있습니다. `fetch` 함수는 백엔드에서 제공하는 `/sound/:animal` API에 GET 요청을 보내고, 백엔드에서 반환된 JSON 응답을 사용하여 결과를 화면에 표시합니다.

이 영상은 Node.js를 처음 접하는 사람들에게 기본적인 설치와 사용법, 그리고 간단한 웹 서버 및 API 구축 방법을 설명하는 데 중점을 두고 있습니다. Express와 같은 주요 모듈을 사용하여 실제로 서버를 구축하고 요청을 처리하는 과정을 통해, 백엔드 개발의 기본 개념을 익힐 수 있습니다. 또한, CORS 설정을 통해 외부와의 데이터 통신을 허용하는 방법과 프론트엔드와의 연동을 학습함으로써, 전체적인 웹 개발 흐름을 이해하는 데 도움이 됩니다. 이러한 기술들을 통해 개발자는 클라이언트와 서버 간의 통신을 원활하게 구현하고, 풀스택 개발의 기본 개념을 확립할 수 있습니다.
