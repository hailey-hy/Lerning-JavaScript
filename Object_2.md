### 1. 생성자로 객체 생성하기

- 자바스크립트에는 클래스가 없는 대신, 생성자로 객체를 생성 가능
- 생성자
    - 정의
        
        <aside>
        💡 new 연산자로 객체를 생성할 것이라 기대하고 만든 함수
        
        </aside>
        
    - 예시
        
        ```jsx
        // 생성자로 객체 생성
        function Card(suit, rank) {
        	this.suit = suit;
        	this.rank = rank;
        }
        
        var card = new Card("하트", "A");
        console.log(card); // Card { suit:"하트", rank:"A" }
        
        //객체 리터럴로 객체 생성
        var card = {};
        card.suit = "하트";
        card.rank = "A";
        ```
        
    - 사용 방법
        - 생성자임을 알리기 위해 첫 글자를 대문자로 사용
        - 생성자 안에서 this.프로퍼티 이름에 값을 대입하면 그 이름을 가진 프로퍼티에 값이 할당된 객체가 생성
    - 생성자의 역할
        - 객체를 생성하고 초기화하는 역할
        - 이름은 같지만 프로퍼티 값이 다른 객체 여러 개를 간단히 생성 가능
            - 예시
                
                ```jsx
                var card1 = new Card("하트", "A");
                var card2 = new Card("클럽", "K");
                var card3 = new Card("스페이드". "2");
                ```
                
        - 함수이므로 프로퍼티에 값을 대입할 수 있으며, 객체 생성 시 초기화 작업 병행 가능
            - 예시
                
                ```jsx
                function Particle(x, y, vx, vy) {
                	this.x = x;
                	this.y = y;
                	this.vx = vx;
                	this.vy = vy;
                	this.velocity = Math.sqrt(vx * vx + vy * vy);
                }
                
                var p = new Particle(0, 0, 3, 4);
                console.log(p); // Particle { x:0, y:0, vx:3, vy:4, velocity:5}
                ```
                
    - 메서드를 가진 객체를 생성하는 생성자
        - 생성자에서 this.프로퍼티 이름에 함수의 참조를 대입
        - this는 생성될 인스턴스를 가리킴
            - 예시
                
                ```jsx
                fucntion Cricle(center, radius){
                	this.cnter = center;
                	this.radius = radius;
                	this.area = function() {
                		return Math.PI * this.radius * this.radius;
                	};
                }
                var p = {x:0, y:0};
                var c = new Circle(p, 2.0);
                console.log("넓이 =" + c.area();
                ```
                

### 2. 내장 객체

- 자바스크립트에서 처음부터 사용할 수 있는 내장 객체
1. 내장 생성자
    1. Date 생성자
        - 날짜와 시간을 표현하는 객체를 생성
        - Date 객체 생성 가능
            - 예시
                
                ```jsx
                var now = new Date();
                console.log(now) // Date {Tue Aug 01 2017 09:12:34 GMT+0900 (KST)}
                ```
                
        - Date 생성자의 인수로 날짜와 시간을 전달하면 그 날짜와 시간을 가리키는 Date 객체가 생성
            - 예시
                
                ```jsx
                var then - new Date(2008, 6, 10);
                console.log(then); // Date { Tue Jun 10 2008 00:00:00 GMT+0900 (KST)}
                ```
                
        - 계산식 적용 시 밀리초 단위 정수로 값의 타입이 바뀌며, 프로그램 실행에 걸리는 시간 측정 가능
            - 예시
                
                ```jsx
                var start = new Date();
                //실행 시간을 측정할 코드
                var end = new Date();
                var elapsed = end - start;
                ```
                
    2. Function 생성자
        - 함수를 생성하는 생성자
            - 예시
                
                ```jsx
                var square = new Function("x", "return x * x");
                ```
                
2. 전역 객체
    - 의미
        - 내장 객체의 한 종류
        - 프로그램 어디에서나 사용할 수 있는 객체
    - 사용
        - 전역 객체의 프로퍼티는 프로그램의 어느 위치에서나 사용 가능
        - 자바스크립터 인터프리터 시작 시 / 웹 브라우저가 새로운 페이지 읽어드릴 때마다 새로운 전역 객체가 생성
        - 전역 객체의 프로퍼티
            
            
            | 분류 | 프로퍼티 |
            | --- | --- |
            | 전역 프로퍼티 | undefined, NaN, Infinity |
            | 생성자 | Object(), String(), Number() |
            | 전역 함수 | parseInt(), parseFloat(), isNan() |
            | 내장 객체 | Math, Json, Reflect |
3. 자바스크립트 객체의 분류
    1. 네이티브 객체
        - ECMAScript 사양에 정의된 객체
        - 내장 생성자로 생성된 객체, JSON, Math, Relect 등
    2. 호스트 객체
        - ECMAScript에는정의되어 있지 않지만 자바스크립트 실행 환경에 정의된 객체
        - 브러우저 객체(Window, Navigator, History, Location), DOM에 정의되어 있는 객체, XMLHttpRequest 객체, HTML5의 각종 API
    3. 사용자 정의 객체
        1. 사용자가 정의한 자바스크립트 코드를 실행한 결과로 생성된 객체