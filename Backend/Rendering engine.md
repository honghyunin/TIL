# 렌더링

HTML, CSS, JavaScript 등 작성된 문서를 브라우저에 출력하는 과정을 말합니다.

# 렌더링 과정

1. HTML, CSS를 다운로드합니다.
2. 다운받은 HTML, CSS => Object Model(객체화하여 사용할 수 있게) 로 만듭니다.
      - HTML -> DOM, CSS -> CSSOM
> DOM과 CSSOM을 이용 -> Rendedr Tree 생성
      ![Rendering Tree](/images/rendreing.png)

> Render Tree에는 실제 화면에 표현되는 노드(요소)들로만 구성됩니다.

3. Layout

- 레이아웃 단계는 *Viewport 내에서 __``브라우저 화면의 어떤 위치에 어떤 크기로 출력될지 계산하는 단계``__ 입니다. 

> Viewport(뷰포트) 그래픽이 표시되는 브라우저의 영역, 크기(사진 참조)

<레이아웃의 나쁜 예시>

![Bad_Layout](/images/Layout1.png)

< 레이아웃의 좋은 예시>

![Good_Layout](/images/layout2.png)

4. Paint
- Layout 계산이 완료되면 요소들을 실제 화면에 그리게 됩니다.

# 정리

> 1. 주소창에 구글을 입력.
> 2. 구글 서버로 찾아간다.
> 3. *DNS가 연결해줄 곳을 찾음
> 4. 서버에서 HTML 파일을 클라이언트로 보냄.
> 5. HTML 파일 파싱 및 DOM Tree 생성
> 6. link 태크를 만나 css 파싱 및 CSSOM 트리 생성
> 7. DOM, CSSOM 합쳐 render Tree 생성
      (8. JavaScript를 만나면? HTML 파서는 JS코드를 실행하기 위해 파싱 중단)
> 8. JS 엔진실행 및 JS 코드 파싱

*DNS : 실제 서버가 어디있는 지 알고 있는 서버