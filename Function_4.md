### 1. 객체로서의 함수

- 자바스크립트에서 함수는 일급 객체의 특징을 가지는 일급 함수
- 일급 객체의 특징
    - 변수, 프로퍼티, 배열 요소에 대입 가능
    - 함수의 인수로 사용 가능
    - 함수의 반환값으로 사용 가능
    - 프로퍼티와 메서드를 가질 수 있음
    - 이름 없는 리터럴로 표현 가능 (익명 함수)
    - 동적으로 생성 가능

### 2. 함수의 프로퍼티

- 함수의 프로퍼티
    
    
    | 프로퍼티 이름 | 설명 |
    | --- | --- |
    | caller  | 현재 실행 중인 함수를 호출한 함수 |
    | length | 함수의 인자 개수 |
    | name | 함수를 표시할 때 사용하는 이름 |
    | prototype | 프로토타입 객체의 참조 |
- Function.prototype(Fucntion 생성자의 Prototype 객체)에서 상속받은 프로퍼티
    
    
    | 프로퍼티 이름 | 설명 |
    | --- | --- |
    | apply() | 선택한 this와 인수를 사용해 함수를 호출
    인수는 배열 객체 |
    | bind() | 선택한 this와 인수를 적용한 새로운 함수 반환 |
    | call() | 선택한 this와 인수를 사용해 함수 호출
    인수는 쉼표로 구분한 값 |
    | constructor | Function 생성자의 참조 |
    | toString() | 함수의 소스 코드를 문자열로 만들어 반환 |
    - apply와 call
        - 결과는 같지만, 인수로 넘길 때 차이가 있음
        - 예시
            
            ```jsx
            function say(greetings, honorifics)_
            	console.log(greetings + " " + honorifics + this.name);
            }
            
            var tom = {name: "Tom"};
            var becky = {name: "Becky};
            
            say.apply(tom, ["Hello", "Mr"]);
            say.apply(becky, ["Hello", "Ms".]);
            
            say.call(tom, "Hello", "Mr.");
            say.call(becky, "Hello", "Ms.");
            ```
            
    - bind
        - 객체에 함수를 속박함
        - 예시
            
            ```jsx
            function say(greetings, honorifics)_
            	console.log(greetings + " " + honorifics + this.name);
            }
            
            var tom = {name: "Tom"};
            var sayToTom = say.bind(tom);
            sayToTom("Hello", "Mr."); // Hello Mr. Tom
            
            //sayToTom은 항상 tom 객체를 함수 say의 this로 설정
            ```
            

### 3. 함수의 프로퍼티 추가

- 예시
    
    ```jsx
    fucntion f(x){...}
    f.p = a;
    f.g = function(){...};
    ```
    

### 4. 콜백 함수

- 정의
    
    <aside>
    💡 다른 함수에 인수로 넘겨지는 함수
    
    </aside>
    
    - 자바스크립트의 함수는 일급 객체이며 다른 함수에 인수로 넘겨질 수 있음
    - 예시
        
        ```jsx
        f(g, ...);
        ...
        function f(callback, ...){
        	...
        	callback();
        	...
        }
        ```
        
        - 함수 f의 인수로 넘겨진 g가 콜백 함수
- 특징
    - 함수를 호출할 때 무언가 새로운 일이 생기거나, 그 함수의 실행이 끝나면 지정한 콜백 함수를 실행해 주도록 함수에 요청해야 할 때 사용
- 예시
    1. 이벤트 처리기
        - 특정 이벤트가 발생했을 때 실행하도록 등록하는 함수
        - 함수를 호출할 때 사건이 발생하면 콜백 함수를 실행
    2. 타이머
        - 타이머 메서드에서 첫 번째 인수로 함수를 넘김