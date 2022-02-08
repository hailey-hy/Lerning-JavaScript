### 1. 함수의 실행 흐름

1. 호출한 코드에 있는 인수가 함수 정의문의 인자에 대입
2. 함수 정의문의 중괄호 안에 작성된 프로그램이 순차적으로 실행
3. return문이 실행되면 호출한 코드로 돌아가며, return문의 값은 함수의 반환값이 됨
4. return문이 실행되지 않은 상태로 마지막 문장이 실행되면 호출한 코드로 돌아간 후 undefined가 함수의 반환값이 됨

### 2. 함수 선언문의 끌어올림

- 자바스크립트 엔진은 함수 선언문을 프로그램의 첫머리로 끌어올림
    - 예시
        
        ```jsx
        console.log(square(5)); // 25
        function square(x){return x * x;)
        ```
        

### 3. 값으로서의 함수

- 자바스크립트에서 함수는 객체
- 함수 선언시, 내부적으로 함수 이름을 이름으로 한 변수와 함수 객체가 생성되며 그 변수에 함수 객체의 참조가 저장됨
    - 예시
        
        
        | square | function 메모리 주소 참조 |
        | --- | --- |
        
        | function(x){ return x*x; } |
        | --- |
- 변수 값을 다른 변수에 할당할 경우, 그 변수 이름으로 함수 실행 가능
    - 예시
        
        ```jsx
        function square(x){return x * x;)
        
        var sq = square;
        console.log(sq(5)); // 25
        ```
        

### 4. 값에 의한 호출과 참조에 의한 호출

1. 값에 의한 호출
    - 원시 값을 함수의 인수로 넘겼을 때, 그 값 자체가 인자에 전달됨
        - =값의 전달
    - 예시
        
        ```jsx
        function add1(x){ return x = x + 1; }
        var a = 3;
        var b = add1(a);
        console.log("a = " + a + ", b = " + b;) // a = 3, b = 4
        ```
        
    - 해석
        - 변수 a의 복사본이 인자 x에 할당
        - 변수 a와 변수 x는 다른 영역의 메모리에 위치한 별개의 변수
2. 참조에 의한 호출
    - 객체를 함수의 인수로 넘겼을 때, 참조 값을 인자에 전달
        - =참조 전달
    - 예시
        
        ```jsx
        function add(p){ p.x = p.x + 1; p.y + 1; return p; }
        var a = {x:3, y:4};
        var b = add1(a);
        console.log(a, b); // Object {x = 4, y = 5} Object {x = 4, y = 5}
        ```
        
    - 해석
        - 인자 p와 변수 a는 똑같은 객체를 참조
        - 함수 안에서 p.x, p.y를 수정하는 행위는 a.x와 a.y를 수정하는 행위와 동일
3. 응용: 인수 여러개를 전달하기
    - 함수에 넘겨야 하는 인수 개수가 많아질 경우, 아래와 같은 문제 발생
        - 인수의 순서를 착각하기 쉬움
        - 인수 개수를 바꿀 경우 함수 호출 방법이 바뀌므로 프로그램 전체를 수정해야 함
    - 해결 방법
        - 객체의 프로퍼티에 인수를 담아서 전달하기
            - 예시
                
                ```jsx
                //변경 전
                function setBallProperties(x, y, vx, vy, radius) {...}
                setBallProperties(0, 0, 10, 15, 5);
                
                // 변경 후
                var parameters = {
                	x: 0, 
                	y: 0, 
                	vx: 10,
                	vy: 15,
                	radius: 5
                };
                
                function seBallProperties(params){...}
                seBallProperties(parameters);
                ```
                

### 5. 변수의 유효 범위

- 유효 범위
    
    <aside>
    💡 변수에 접근할 수 있는 범위
    
    </aside>
    
- 유효 범위에 따른 자바스크립트의 변수 구분
    1. 전역 변수
        - 정의
            
            <aside>
            💡 함수 바깥에서 선언된 변수로, 유효범위가 전체 프로그램
            
            </aside>
            
    2. 지역 변수
        - 정의
            
            <aside>
            💡 함수 안에서 선언된 변수로, 유효범위는 변수가 선언된 함수 내부
            
            </aside>
            
- 함수의 충돌
    - 전역 변수 이름과 지역 변수 이름이 같을 경우 발생
    - 충돌 발생 시 전역 변수를 숨기고 지역 변수를 사용
        - 예시
            
            ```jsx
            var a = "global";
            function f() {
            	var a = "local"; 
            	console.log(a); //local
            	return a;
            }
            f();
            console.log(a); //global
            ```
            
- 함수 안에서의 변수 끌어올림
    - 함수 중간 부분에서 변수를 선언해도 변수의 선언부는 함수 첫머리로 끌어올려짐
        - 예시
            
            ```jsx
            function f() {
                console.log(a); //undefined
                var a = "local";
                console.log(a); //local
                return a;
            }
            ```
            
- 함수 안에서의 변수 선언 생략
    - 변수를 선언하지 않은 상태에서 값을 대입할 경우 전역 변수로 선언
        - 예시
            
            ```jsx
            function f() {
                a = "local";
                console.log(a); // local
                return a;
            }
            f();
            console.log(a); // local
            ```
            

### 6. 블록 유효 범위

- 블록 유효 범위를 가진 변수는 블록 ({})안에서만 유효
1. let 선언자
    - 블록 유효 범위를 갖는 지역 변수를 선언
    - 예시
        
        ```jsx
        let x;
        let a, b, c;
        let x = 5, y = 7;
        ```
        
2. const 선언자
    - const문: 블록 유효 범위인 동시에 한 번만 할당할 수 있는 변수를 선언
    - 반드시 초기화 해야 함
        - 예시
            
            ```jsx
            const c = 2;
            c = 5; // Uncaught TypeError
            ```
            
    - const로 선언한 상수 값이 객체이거나 배열일 경우 프로퍼티 값 수정 가능
        - 예시
            
            ```jsx
            const origin = {x:1, y:2};
            origin.x = 3;
            console.log(origin);
            ```
            

### 7. 함수 리터럴로 함수 정의

- 함수 리터럴로 함수 정의 예시
    
    ```jsx
    var square = function(x) { return x * y; };
    ```
    
    - 해석
        - {} 부부이 함수 리터럴
        - 함수 리터럴 = 익명 함수, 무명 함수
        - 함수 선언문에서와는 달리 함수 리터럴을 사용할 때는 세미콜론 반드시 필요

### 8. 객체의 메서드

- 메서드
    
    <aside>
    💡 객체의 프로퍼티 중 함수 객체의 참조를 값으로 담고 있는 프로퍼티
    
    </aside>
    
- 선언 방법
    - 프로퍼티 값으로 함수 리터럴을 대입
- 예시
    
    ```jsx
    var circle = {
    	center: {x:1.0, y:2.0}
    	radius: 2.5,
    	area: function () {
    		return Math.PI * this.radius * this.radius;
    	}
    };
    
    circle.area() //19.63495...
    ```
    
- 해석
    - this: 함수를 메서드로 가지고 있는 객체
    - this.radius = circle.radius
    - circle.area()로 실행 가능
- 메서드 추가
    - 메서드 또한 프로퍼티의 일종이므로 나중에 추가할 수 있음
        - 예시
            
            ```jsx
            circle.translate = function(a, b) {
            	this.center.x = this.center.x + a;
            	this.center.y = this.cetner.y + b;
            };
            
            circle.translate(1, 2);
            circle.center; // Object { x = 2, y = 4}
            ```