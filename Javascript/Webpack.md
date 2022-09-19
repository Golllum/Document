## Webpack : Module Bundler

- webpack 이란?
    - webpack 이란 오픈 소스 자바스크립트(JS) 정적 모듈 번들러이다.
        - 모듈 번들러란 웹 애플리케이션을 구성하는 자원(HTML, CSS, Javscript, Images 등)을 모두 각각의 모듈로 보고 이를 조합해서 병합된 하나의 결과물을 만드는 도구를 의미한다. 
        - webpack 이란, 여러 파일을 하나 이상의 파일로 합쳐주는 자바스크립트 번들러이다.
    - 다양한 호환 플러그인과 로더 등을 함께 조합하여 js 뿐만 아니라 css, html, 이미지 등 다양한 Frontend resource 들을 번들링하여 정적 resource를 생성한다.
    - 웹팩은 의존성을 취한 다음 의존성 그래프를 만듦으로써 웹 개발자들이 웹 애플리케이션 개발 목적을 위해 모듈 방식의 접근을 사용할 수 있게 도와준다.
    - webpack.config.js 파일을 생성하여 webpack 및 devServer 등 설정을 할 수 있다.
    - Weppack, Broserify, Parcel 과 같은 도구들이 번들러에 속한다.

<br></br>

- 모듈 번들러의 등장배경  
    웹사이트를 구성할때 .js .css .images 파일 등 수 많은 들이 모여 웹사이트를 구성하게 된다. 따라서 웹사이트에 접속했을때 굉장히 많은 파일이 다운로드 될 수 있는데 이것에 비례하여 서버의 자원을 소모하고 웹사이트가 느리게 로딩이 된다. 또한, 많은 자바스크립트 패키지등을 사용하다보면 각각의 서로 다른 패키지들이 서로 같은 이름이나 함수를 사용하게 되면서 애플리케이션이 깨지게 되는데 이러한 현상을 해결하기 위해 나온 개념이 묶는다는 개념의 번들러가 등장하였다.

    자바스크립트에서는 ES2015(ES6) 이전에는 모듈로서 관리하는 방법으로 AMD, CommonJs 등이 존재했으나 하나의 표준이 아닌 사용하는 사람에 따라 원하는 것을 선택하는 방식으로 사용해왔다.

    그 후, ES6 이후부터 자바스크립트에서 표준 모듈 시스템을 제안하였고 이것이 export/import 방식이다. 그러나 모든 모든 브라우저에서 ES6 방식의 모듈 시스템을 지원하지는 않았다. 따라서 개발자들은 브라우저와 버전에 상관없이 편리한 모듈 시스템을 사용하기르 원했고 이러한 배경에 의해 등장하게된 툴이 웹팩이다.

    < 정리 >
    - 파일 단위의 자바스크립트 모듈 관리의 필요성
    - 웹 개발 작업 자동화 도구 (Web Task Manager)
    - 웹 애플리케이션의 빠른 로딩 속도와 높은 성능  

<br></br>

- webpack 에서의 module 이란,
    - 웹팩에서 지칭하는 모듈은 자바스크립트 모듈 뿐만이 아닌 HTML, CSS, JS, Images, Font 등 모든 파일 하나하나 모듈이라 지칭하며 웹 애플리케이션을 구성하는 모든 자원을 모듈이라 보면 된다. 
    - 보통 모듈 번들링에서는 빌드, 번들링, 변환 이 세 단어는 모두 같은 의미로 사용된다고 한다.

<br></br>

- webpack 핵심요소
    - Entry
        - Entiry 속성은 웹팩에서 웹 자원을 변환하기 위해 필요한 최초 진입점이다.
        - Entry로 묶고자하는 파일의 첫번째 진입점을 설정해주면 된다.
            ```
            // webpack.config.js

            // Single Page Application(SPA)
            module.exports = {
                entry: './src/index.js'
            }

            // Multi Page Application (MPA)
            module.exports = {
                entry: {
                    login: './src/LoginView.js',
                    main: './src/MainView.js'
                }
            }
            ```
        - 최초 진입점이 되는 대상 파일은 웹 애플리케이션의 전반적인 구조와 내용이 담겨있어야 한다. 그래야 웹팩이 해당 파일을 토대로 애플리케이션의 모듈들의 연관관계에 대해 이해하고 분석하고 합치기 때문이다.
        - webpack 빌드 후 dependency graph가 생기는데 이는 모듈 간 의존성 구조를 그래프로 표현한 것이다.
    - Output
        - 웹팩을 실행하여 빌드하고 난 후 결과물의 파일 경로를 의미한다.
        - filename 속성은 웹팩으로 빌드한 파일의 이름을 의미하며 여러가지 옵션을 넣을 수 있다.
        - path 속성은 해당 파일의 경로를 의미한다. 여기서 path 속성에서 사용된 메서드는 인자로 받은 경로를 조합하여 유효한 파일 경로를 만드는 NodsJS API라고 한다.
            ```
            // webpack.config.js
            var path = require('path');

            module.exports = {
                output: {
                    filename: 'bundle.js',
                    path: path.resolve(__dirname, './dist')
                }
            }

            /* NodeJS API가 하는 역할은 아래 코드와 동일하다. */
            output: './dist/bundle.js'
            ```
    - Loader
        - 웹팩이 애플리케이션을 해석할때 자바스크립트 파일이 아닌 HTML, CSS, Images, font 등을 변환할 수 있게 도와주는 속성이다. 웹팩은 모든 파일을 모듈로 취급하여 관리하는데 사실상 자바스크립트 파일만 알고 있어 로더를 이용해 다른 파일들을 웹팩이 이해하게끔 변경해줘야 한다.
        - 웹팩 설정 파일에 로더를 설정을 지정해주지 않으면 웹팩이 해당 파일을 읽을 수 없기 때문에 에러가 발생한다.
        - 로더 설치 후, 로더 설정 파일에도 어떤 파일 형식들을 로딩할 것인지 기입해야한다.
            ```
                module.exports = {
                    module: {
                        rules: [
                        { test: /\.css$/, use: 'css-loader' },
                        { test: /\.ts$/, use: 'ts-loader' },
                        // ...
                        ]
                    }
                }
            ```

    - Plugin
        - 웹팩의 기본적인 동작에 추가적인 기능을 제공하는 속성이다.
        - 로더는 파일을 해석하고 변환하는 과정에 관여하며, 플러그인은 해당 결과물의 형태를 바꾸는 역할을 한다고 볼 수 있다.
            > HtmlWebpackPlugin : 웹팩으로 빌드한 결과물로 HTML 파일을 생성해주는 플러그인  
            > ProgressPlugin : 웹팩의 빌드 진행율을 표시해주는 플러그인
            ```
            // webpack.config.js
            var webpack = require('webpack');
            var HtmlWebpackPlugin = require('html-webpack-plugin');

            module.exports = {
                plugins: [
                    new HtmlWebpackPlugin(),
                    new webpack.ProgressPlugin()
                ]
            }
            ```

<br></br>

- webpack 활용
    - 자바스크립트 변수 유효 범위 문제
        - ES6의 모듈 문법과 번들링으로 해결
    - 브라우저별 HTTP 요청 숫자의 제약
        - TCP 스펙에 따라 브라우저에서 한 번에 서버로 보낼 수 있는 HTTP 요청 숫자는 제약되어 있다.
        - http/2에서는 하나의 커넥션에 동시에 여러 파일들을 요청할 수 있지만, 우리가 주로 사용하는 http/1.1에서는 하나의 커넥션에서 하나씩 요청을 보내야 한다. 예를들어 하나의 웹 사이트에서 사용하는 자바스크립트 파일이 10개라면 로드될때마다 10개를 모두 네트워크 요청을 통해 받아와야 하며 프로젝트 규모가 커질 수록 병목현상을 야기시키는 요소 중 하나이다. 웹팩은 여러 파일을 하나 이상의 파일로 합쳐 맨 처음 언급하였던 서버로 부터 파일을 다운로드 받는 횟수가 줄어들게 되고 이 효과로 인해 브라우저별 HTTP 요청 숫자 제약을 피할 수 있다.
    - 사용하지 않는 코드의 관리
    - Dynamic Loading 및 Lazy Loading 미지원 문제
        - 이전에는 Require.js 같은 라이브러리를 사용하지 않는 이상 동적으로 원하는 순간에 모듈을 로딩하는 것이 불가능 했다. 웹팩에서는 Code Splitting 기능을 이용하여 원하는 모듈을 원하는 타이밍에 로딩할 수 있다