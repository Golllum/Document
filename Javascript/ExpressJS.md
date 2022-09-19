## ExpressJS

- express.js 특징

  - node.js의 표준 서버 프레임워크라고 불린다.
  - node.js의 핵심 모듈인 http와 Connect 컴포넌트를 기반으로 하는 웹 프레임워크다.

- express.js 작동방식

  - 보통 express.js에는 메인 파일이라고 하는 진입점이 있다. 메인 파일에서는 다음과 같은 단계를 밟는다.
    ```
    1. 컨트롤러, 유틸리티, 도우미, 모델과 같은 자체적인 모듈을 비롯한 서드파티 의존 모듈을 인클루드한다.
    2. 템플릿 엔진과 해당 템플릿 엔진의 파일 확장자와 같은 Express.js 앱 설정을 구성한다.
    3. 오류 핸들러, 정적 파일 폴더, 쿠키 및 기타 파서와 같은 미들웨어를 정의한다.
    4. 라우팅을 정의한다.
    5. MongoDB, Redis 또는 MySQL과 같은 데이터베이스에 연결한다.
    6. 앱을 구동한다.
    ```
  - Express.js 앱이 실행되면 Express.js가 요청을 대기한다.
  - 앱으로 들어오는 각 요청은 정의된 미들웨어와 라우팅에 따라 맨 위에서 시작해 맨 아래까지 처리된다.
    ```
    1. 쿠키 정보를 파싱하고, 파싱이 완료되면 다음 단계로 이동한다.
    2. URL로부터 매개변수를 파싱하고, 파싱이 완료되면 다음 단계로 이동한다.
    3. 사용자가 인증되면(쿠키/세션) 매개변수의 값을 토대로 데이터베이스에서 정보를 가져와 일치하는 것이 있으면 다음 단계로 이동한다.
    4. 데이터를 표시하고 응답을 마친다.
    ```

- express.js 사용예시

  ```
  var express = require('express');
  var port = 3000;
  var app = express();

  app.get('/name/:user_name', function(req,res) {
  res.status(200);
  res.set('Content-type', 'text/html');
  res.end('<html><body>' +
      '<h1>Hello ' + req.params.user_name + '</h1>' +
      '</body></html>'
  );
  });

  app.get('*', function(req, res){
  res.end('Hello World');
  });

  app.listen(port, function(){
  console.log('The server is running, ' +
      ' please open your browser at http://localhost:%s',
      port);
  });
  ```
