### 1. 문자열 연결

- 피연산자가 모두 문자열이라면 + 연산자로 연결
    - 예시
        
        ```jsx
        "Hello " + "World!" // "Hello World!"
        ```
        
- 피연산자 중 하나가 문자열 또는 문자열로 변환될 수 있는 객체일 경우, 문자열로 바꾼 후 연결
    - 예시
        
        ```jsx
        10 + " little indians" // "10 little indians"
        1 + {} // "1[object Object]"
        ```
        

### 2. 문자열 조작 메서드

- 문자열 처리를 위해 문자열을 String 객체로 변환
    - String 메서드를 사용하여 래핑
        - 래핑: 원시 값을 객체로 변환하는 행위
    - 예시
        
        ```jsx
        var msgObj = new String("Everything is practice.");
        ```
        
    - 문자열에서 프로퍼티를 사용시 자동으로 String 객체로 변환되므로 생략 가능
        - 동작 예시
            
            ```jsx
            var msg = "Everything is practice."
            var c = msg.charAt(3);
            
            //내부적으로 아래 코드 실행
            var msgObj = new String(msg);
            var c = msgObj.charAt(3);
            ```
            
            → msgObj는 래퍼 객체
            
            - 래퍼 객체: 일시적으로 생성되는 Stirng 객체로 처리가 끝나면 메모리에서 삭제됨
- 문자열의 길이 구하기: length 프로퍼티 사용
    - 예시
        
        ```jsx
        var msgObj = new String("Everything is practice.");
        msgObj.length // 23
        ```
        
- n 번째 문자 구하기: charAt() 메서드 사용
    - 예시
        
        ```jsx
        var msgObj = new String("Everything is practice.");
        msgObj.charAt(3) // "r"
        ```
        
- 객체 변환된 원시 값을 다시 문자열로 출력하기: valueOf() 메서드 사용
    - 예시
        
        ```jsx
        var msgObj = new String("Everything is practice.").valueOf();
        console.log(msg); // Everything is practice.
        
        //사용하지 않는다면
        var msgObj = new String("Everything is practice.");
        console.log(msg); // String {[[PrimitiveBalue]]: "Everything is practice."}
        ```
        
- 자바스크립트의 문자열은 불변

### 3. String 생성자의 프로퍼티

| 프로퍼티 | 설명 |
| --- | --- |
| String.length | 항상 1 |
| String.fromCharCode() | 인수로 넘긴 문자 코드 목록으로 문자열을 만들어 반환 |
| String.fromCodePoint() | 인수로 넘긴 코드 포인트 목록으로 문자열을 만들어 반환 |
| String.prototype | String의 프로토 타입 객체 |
| String.raw() | 템플릿 문자열의 원시 문자열 형식을 반환 |
- String.fromCharCode로 써로게이트 페어 구하기
    - 써로게이트 페어: UTF-16의 인코딩 값 두 개를 한 쌍으로 묶은 것
    - 예시
        
        ```jsx
        String.fromCharCode(0xd83d,0xdcd6)
        ```
        
    - 특징
        - 써로게이트 페어의 다섯 자릿수 코드 포인트 표현은 지원하지 않음
        - 코드 포인트 스칼라 값을 인수로 넘겨도 반환

### 4. 문자열을 배열로 읽고 쓰기

- 문자열을 읽을 때 대괄호 연산자 사용 가능
    - 예시
        
        ```jsx
        var msg = "Everything is practice."
        
        msg[3] // "r"
        msg[msg.length - 1] // "."
        ```
        
- 그러나 값을 대입해 수정 불가