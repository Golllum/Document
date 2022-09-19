## JPA Error

```
1. cannot resolve column "user_id"
[원인] JPA 어노테이션 값이 DB와 연동되지 않아서 발생
[해결] Assign Data Source 설정 필요

2. raw use of parameterized class "responseEntity"
[원인] Raw Type Generic 이슈 : 제네릭 타입을 지정하지 않아서 발생
[해결] <?> 제네릭 타입 지정
```

## React

```
1. Assign arrow function to a variable before exporting as module default
[원인] Component export 하기 위해서는 리터럴 함수 및 변수 할당이 필요함
[해결] export function 형태가 되어야함
        1) const someting = () => {}; export default something;
        2) export default function something(){};

2. Cannot use import statement outside a module
[원인] NodeJS 최신 버전의 경우 ES6 문법을 대부분 지원하지만 CommonJS 기반 모듈 시스템을 디폴트로 사용하기 때문에
       ES6 모듈 시스템 문법인 import, export 키워드 등을 사용할 때 에러가 발생한다.
[해결] require 키워드를 사용하여 CommonJS 모듈 시스템을 사용하거나, bable과 같은 transpiler를 설치하여 사용한다.

3. Client does not support authentication protocol requested by server; consider upgrading MYSQL client
[원인] Client 프로그램에서 mysql 패스워드 플러그인 "caching_sha2_password"를 해석하지 못해서 발생한다.
[해결] ALTER USER '아이디'@'호스트' IDENTIFIED WITH mysql_native_password BY '비밀번호'

4. You may need an approproate loader to handle this file type, currently no loaders are configured to process this file. See https://webpack.js.org/concepts#loaders
[원인] module bundler 사용 시, js 외 다른 파일들을 함께 번들링 할 때 loader 설정이 되어있지 않아서 발생
[해결] loader 설치 및 bundler 설정 파일에 loader 설정 추가 (webpack.config.js 등)
```

## VCS

- GitHub
  ```
  1. local existing project initial push
     vsc : initialize repository > staging > commit > publish branch > new repository name 기입
  ```

## WEB

```
1. No 'Access-Control-Allow-Origin' header is present on the requested resource.
[원인] SOP (Same Origin Policy) 로 인해 발생
         1) Javascript 엔진 표준 스펙에 있는 동일 출처 정책(SOP)이라는 보안규칙으로 인해 발생한다.
         2) Javascript 로 다른 웹페이지에 접근할 때는 같은 출처 (프로토콜, 호스트명, 포트) 의 페이지에만 접근 가능하다.
         3) REST API 등 외부 공개 API의 호출이 많아지는 환경으로 인해 CORS(Cross Origin Resource Sharing) 정책이 추가되었다.
[해결] BE Server CORS 설정을 통해 해결
         1) WebMvcConfigure 인터페이스를 구현하고 @Configuration 어노테이션을 가진 클래스를 하나 만들어서 설정한다.
         @Configuration
         public class WebConfig implements WebMvcConfigure {
            @Overried
            public void addCorsMappings(CorsRegistry registry){
               registry.addMapping("/**")
                     .allowedOrigins("http://localhost:3000")
                     .allowedMethods("*")
                     .allowedHeaders("*")
                     .allowedCredentials(true); // client에서 credential 설정이 되어있는 경우
            }
         }
```

## ETC

```

1. port Error : Web server failed to start. Port 8080 was already in use.
   [윈인] 포트 중복사용으로 인한 서비스 시작 안되는 이슈
   [해결] 해당 포트 kill 필요 1) cmd : netstat -ano OR netstat -ano | findstr [portNum] : PID 확인 2) cmd : taskkill /F /pid [process_id]

2. mysql Error : access denied for user 'root'@'localhost' (using password: yes)
   [원인] root 계정 권한 및 정보 설정 오류
   [해결] DB 설정 Sync 필요 1) root 계정의 권한 설정 2) root 계정의 비밀번호가 application.properties와 해당 DB가 서로 다름

```
