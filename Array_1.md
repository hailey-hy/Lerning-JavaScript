### 1. 배열 리터럴로 생성하기

- 배열 리터럴이란
    - 쉼표로 구분한 값을 대괄호로 묶어서 표현
        - 예시
            
            ```jsx
            var evens = [ 2, 4, 6, 8];
            ```
            
- 배열 리터럴의 특징
    - 자바스크립트의 배열은 객체 타입으로, 변수에 배열을 대입하면 배열의 참조가 변수에 저장됨
    - 배열 안에 어떤 요소도 작성하지 않을 경우 빈 배열 생성
    - 배열 리터럴 요소의 값을 생략하면 해당 요소는 생성되지 않음
        - 예시
            
            ```jsx
            var a = [2, , 4];
            console.log(a); // [2, undefined, 4]
            ```
            

### 2. length 프로퍼티

- 배열의 길이를 의미
- 배열의 length 프로퍼티에는 배열 요소의 최대 인덱스 값 + 1이 담겨 있음
    - 예시
        
        ```jsx
        var evens = [2, 4, 6, 8]
        evens.length // 4
        ```
        
- 배열 길이를 넘는 인덱스 번호에 할당된 배열 요소는 삭제됨
    - 예시
        
        ```jsx
        var a = ["A", "B", "C", "D"];
        a.length = 2;
        console.log(a); // ["A", "B"]
        ```
        

### 3. Array 생성자로 생성하기

- 예시
    
    ```jsx
    var evens = new Array(2, 4, 6, 8);
    var empty = new Array();
    var a = new Array(2, 4);
    var various = new Array(3.14, "pi", true, {x:1, y:2}, [2, 4, 6, 8]);
    ```
    
- 주의사항
    - Array 생성자의 인수가 양의 정수 한 개라면 정수만큼의 배열 길이를 가진 배열이 생성됨
        - 예시
            
            ```jsx
            var x = new Array(3);
            console.log(x.length); // 3
            ```
            
    - Array 생성자의 인수가 한 개고 그 값이 양의 정수가 아니면 오류 발생
        - 예시
            
            ```jsx
            var x = new Array(-3);
            ```
            
    - 자바스크립트의 배열은 Array의 객체이며, Array 객체는 배열의 인덱스를 문자열로 변환해서 프로퍼티로 이용함
        - 예시
            
            ```jsx
            var a = ["A", "B"];
            console.log(a["1"]); // "B"
            ```
            
    - 배열이 객체이므로, 객체에 없는 프로퍼티를 읽으려고 시도하면 Undefined가 반환

### 4. 배열 요소의 추가와 삭제

- 배열 요소의 추가
    - 없는 배열 요소에 값을 대입해서 추가
        - 예시
            
            ```jsx
            var a = ["A", "B", "C"];
            a[3] = "D";
            console.log(a); // ["A", "B", "C", "D"]
            ```
            
    - push 메서드를 사용해 배열 끝에 추가
        - 예시
            
            ```jsx
            var a = ["A", "B", "C"];
            a.push("D");
            console.log(a); // ["A", "B", "C", "D"]
            ```
            
- 배열 요소를 삭제
    - delete 연산자를 사용해 특정 배열 요소를 삭제
        - 예시
            
            ```jsx
            delete a[1]; 
            console.log(a); // ["A", undefined, "C", "D"]
            ```
            
            → 요소를 삭제해도 배열의 length 프로퍼티 값은 바뀌지 않음
            

### 5. 희소 배열

- 정의
    
    <aside>
    💡 배열에 요소를 추가/제거해서 인덱스가 0부터 시작되지 않는 배열
    
    </aside>
    
- 예시
    
    ```jsx
    var a = ["A", "B", "C"];
    a[4] = "E";
    console.log(a); // ["A", "B", "C", undefined, "E"]
    ```