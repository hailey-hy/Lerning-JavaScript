### 1. 대화 상자

- 정의
    - 입력을 하거나 메세지를 확인하기 위해 별도로 여는 창
- 구성
    - 웹 브라우저의 전역 객체인 Window 객체에는 대화상자 표시를 위한 메서드 세 개 존재
        
        
        | 메서드 | 설명 |
        | --- | --- |
        | window.alert | 경고 대화상자를 표시 |
        | window.prompt | 사용자의 문자열 입력을 받는 대화상자를 표시 |
        | window.confirm | 확인 버튼과 취소 버튼이 있는 대화상자를 표시 |
- 특징
    - 대화상자는 모달 창
        - 모달: 모달 창이 떠 있는 중에는 부모 창의 작업이 일시적으로 정지 상태가 되어 부모 창을 조작할 수 없음
    - 대화상자에는 일반 텍스트만 표시할 수 있으며, 줄 바꿈 문자는 이스케이프 시퀀스로 표현
    - window 객체는 window. 부분을 생략하고 호출할 수 있음

### 2. alert: 경고 대화 상자

- alert 메서드의 정의
    
    <aside>
    💡 경고 대화상자를 표시
    
    </aside>
    
- 특징
    - 인수로 경고 문자열을 받음
    - 대화상자의 확인 버튼을 누르면 대화상자가 사라지고 코드 제어권이 호출한 부분으로 돌아감
- 예시
    
    ```jsx
    alert("안녕하세요");
    ```
    

### 3. prompt: 입력 대화상자

- 정의
    
    <aside>
    💡 입력 대화상자를 표시
    
    </aside>
    
- 특징
    - 인수로 입력을 보조하는 문자열을 받음
    - 사용자로부터 입력받은 문자열은 prompt 메서드의 반환값이 됨
    - 두 번째 인수로 초기 입력값을 지정할 수 있음
    - 반환값은 문자열이므로 parseInt/parseFloat 메서드를 활용해 숫자로 바꾸기 가능
- 예시
    
    ```jsx
    var name = prompt("이름을 입력하십시오"
    var name = prompt("이름을 입력하십시오", "홍길동");
    var age = parseInt(prompt("나이를 입력하십시오"));
    ```
    

### 4. confirm: 확인 대화상자

- 정의
    
    <aside>
    💡 확인 버튼과 취소 버튼이 있는 확인 대화상자를 표시
    
    </aside>
    
- 특징
    - 인수로 메시지를 뜻하는 문자열을 받음
    - 논리값을 반환
        - 확인 버튼 → true 반환
        - 취소 버튼 → false 반환
- 예시
    
    ```jsx
    var ret = confirm("링크를 표시하시겠습니까?")
    ```
    

### 5. console

1. console 객체의 메서드
    - 특징
        - 웹 브라우저와 Node.js 등 다양한 실행 환경에서 사용 가능
        - 콘솔 출력을 돕는 다양한 기능 제공
    - 주요 메서드
        
        
        | 메서드 | 설명 |
        | --- | --- |
        | console.dir | 객체의 대화형 목록을 출력 |
        | console.error | 오류 메세지를 출력 |
        | console.info | 메시지 타입 로그를 출력 |
        | console.log | 일반 로그를 출력 |
        | console.time | 처리 시간 측정용 타이머를 시작 |
        | console.timeEnd | 처리 시간 측정용 타이머를 정지
        타이머 시작 후 흐른 시간을 밀리초 단위로 출력 |
        | console.trace | 스택 트레이스를 출력 |
        | console.warn | 경고 메시지를 출력 |
2. 콘솔에 텍스트 출력하기
    - 방법
        - console.log, console.info, console.warn, console.error 메서드를 사용
    - 특징
        - 인수 여러 개를 쉼푤 구분해서 넘길 수 있음 → 공백 구분
        - 서식 문자열 사용 가능
    - 예시
        
        ```jsx
        var a = [2, 4, 6];
        console.log(("배열", a, "의 길이는", a.length, "입니다.");
        
        var name. ="Tom";
        var height = 172.5;
        console.log("그의 이름은 %s이며 키는 %f입니다.", name, height);
        ```