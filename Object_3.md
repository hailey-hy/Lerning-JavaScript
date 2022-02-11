### 1. 프로토타입의 고안

- 생성자 안에서 메서드를 정의하는 방식의 문제점이 있기 때문
- 생성자 안에서 THis 뒤에 메서드를 정의할 경우, 생성자로 생성한 모든 인스턴스에 똑같은 메서드가 추가됨
- 인스턴스를 여러 개 생성한다면 같은 작업을 하는 메서드를 인스턴스 개수만큼 생성할 것이며, 메모리 낭비로 이어짐
    - 예시
        
        ```jsx
        function Circle(center, radius){
        	this.center = center;
        	this.radius = radius;
        	this.area = function(){
        		return Math.PI * this.radius * this.radius;
        }
        
        var c1 = new Circle({x:0, y:0}, 2.0);
        var c2 = new Circle({x:0, y:1}, 2.0);
        var c3 = new Circle({x:1, y:0}, 2.0);
        // c1, c2, c3 모두 똑같은 메서드 area를 소유
        ```
        

### 2. 프로토타입 객체

- 프로토타입의 정의
    - 원형이 되는 구조
    - 인스턴스에 아무것도 정의하지 않더라도 처음부터 사용할 수 있는 것
- 프로토타입 객체의 프로퍼티
    - 함수 객체가 기본적으로 가짐
        - 예시
            
            ```jsx
            function f(){};
            console.log(F.prototype); // Object {}
            ```
            
            - f의 함수 객체
                
                
                | caller | null |
                | --- | --- |
                | length | 0 |
                | name | “f” |
                | prototype | 프로토타입 객체 참조
                (기본적으로 빈 객체) |
                | __poroto__ | ... |
    - 생성자로 생성한 모든 인스턴스에서 그 인스턴스의 프로퍼티처럼 사용 가능
        - 예시
            
            ```jsx
            function f(){};
            f.prototype.prop = "prototype value";
            var obj = new f();
            console.log(obj.prop); //prototype value
            ```
            
    - 읽기만 가능하고 수정은 불가능하므로, 이름이 같은 프로퍼티가 있을 경우 값만 대입
        - 예시
            
            ```jsx
            function f(){};
            f.prototype.prop = "prototype value";
            var obj = new f();
            obj.prop = "instance value";
            
            console.log(obj.prop); // instance value
            console.log(f.prototype.prop);prototype value
            ```
            
    - 생성자의 프로토타입 객체에 메서드 추가
        - 인스턴스마다 메서드가 생기는 것을 막아 메모리 낭비를 방지
        - 예시
            
            ```jsx
            function Circle(center, radius){
            	this.center = center;
            	this.radius = radius;
            }
            
            Circle.prototype.area = function(){
            	return Math.PI * this.radius * this.radius;
            }
            
            var c1 = new Circle({x:0, y:0}, 2.0);
            var c2 = new Circle({x:0, y:1}, 2.0);
            var c3 = new Circle({x:1, y:0}, 2.0);
            
            console.log("넓이 = " + c1.area());
            ```
            
            - 해석
                - 인스턴스에는 area메서드가 존재하지 않지만 프로토타입 객체의 area 메서드 사용 가능