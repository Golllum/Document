## [ NodeJS ]

- Server Side Javascript 이며, Javascript를 이용한 서버 개발이 가능하다.
- 이벤트 기반 개발이 가능하며, non-blocking I/O를 지원하므로 비동기식 프로그래밍이 가능하다.
- Node.js는 V8 엔진 기반의 JS 런타임(실행기)이며, WAS 기능을 구현할 수 있다.

- npm : Node Package Manager
    - Javascript 런타임 환경 NodeJS의 기본 패키지 관리자이다.
    - command line client (npm) 과 온라인 패키지 데이터베이스 (npm registry) 로 이루어져 있다.
    - node package 들을 모아둔 저장소라고 볼 수 있다.
    - npm 사용을 위해서는 package.json 파일이 필요하며 해당 파일 안에 npm으로부터 주입된 의존성 정보 및 script 명렁어 등의 정보들을 관리한다.
        > npm init : package.json 생성  
        > npm install : 패키지를 프로젝트에 설치(node_modules에 패키지 설치, package.json에 의존성 정보 저장)  
        > npm update : 패키지를 업데이트  
        > npm root : node_modules의 위치 반환
        > npm ls : 현재 설치된 패키지의 버전과 dependencies를 트리구조로 표현  
        > npm ls [패키지명] : 해당 패키지 존재여부와 해당 패키지가 어떤 패키지의 dependencies인지 알려줌  
        > npm ll : npm ls의 상세버전  
        > npm run : package.json script 내 특정 명령어를 실행