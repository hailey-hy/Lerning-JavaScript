### 1. 함수 정의하기

1. 함수 선언문으로 정의하는 방법
    
    ```jsx
    function square(x){return x*x;}
    ```
    
    - 함수 선언문이 끌어올려지므로 호출문이 앞에 위치해도 사용 가능
2. 함수 리터럴로 정의하는 방법
    
    ```jsx
    var square = function(x){return x*x;}
    ```
    
3. Function 생성자로 정의하는 방법
    
    ```jsx
    var square = new function("x":"return x*x");
    ```
    
4. 화살표 함수 표현식으로 정의하는 방법
    
    ```jsx
    var square = x => x*x;
    ```
    

### 2. 중첩 함수

- 정의
    
    <aside>
    💡 특정 함수의 내부에 선언된 함수
    
    </aside>
    
- 특징
    - 외부 함수의 최상위 레벨에만 중첩 함수 작성 가능
- 예시
    
    ```jsx
    function norm(x){
    	var sum2 = sumSquare();
    	return Math.sqrt(sum2);
    	function sumSquare(){
    		sum = 0;
    		for(var i = 0; i < x.length; i++) sum += x[i]*x[i];
    		return sum;
    	}
    }
    var a = [2, 1, 3, 5, 7];
    var n = norm(1);
    console.log(n); // 9.38083...
    ```
    

### 3. 함수 호출하기

- 함수 호출 방법
    1. 함수 호출
        - 함수의 참조가 저장된 변수 뒤에 그룹 연산자인 ()를 붙여 호출
        
        ```jsx
        var s = square(5);
        ```
        
    2. 메서드 호출
        - 메서드: 객체의 프로퍼티에 저장된 값이 함수 타입인 프로퍼티
        
        ```jsx
        obj.m = function(){...}
        obj.m();
        ```
        
    3. 생성자 호출
        
        ```jsx
        var obj = new Object();
        ```
        
    4. call, apply를 사용한 간접 호출
- 즉시 실행 함수
    - 익명 함수를 정의하고 곧바로 실행
        - 예시
            
            ```jsx
            // 일반적 호출
            var f = function(){...};
            f();
            
            //즉시 실행
            (function() {...})();
            ```
            
    - 즉시 실행 함수에도 이름을 붙일 수 있으나, 함수 내부에서만 유효
        - 예시
            
            ```jsx
            (function fact(n){
            	if(n<=1> return 1;
            	return n*fact(n-1);
            })(5);
            ```
            
    - 함수 실행 결과를 변수에 할당 가능
        - 예시
            
            ```jsx
            var x = (function(){...}();
            ```
            

### 4. 함수의 인수

1. 인수의 생략
    - 함수 정의식에 작성된 인자 개수보다 인수를 적게 전달해서 함수를 실행하면 인수에서 생략한 인자는 undefined가 됨
        - 예시
            
            ```jsx
            function f(x, y){
            	console.log("x = " + x + ", y = " + y);
            }
            f(2);
            ```
            
    - 인수를 생략했을 때 사용할 초깃값 설정하기
        - 예시
            
            ```jsx
            function multiply(a, b){
            	b = b || 1;
            	return a * b;
            }
            multiply(2, 3); // 6
            multiply(2); // 2
            ```
            
            → ||: 왼쪽 피연산자가 True로 평가되면 왼쪽을 반환하고, false로 평가되면 오른쪽을 반환
            
2. Arguments 객체
    - 정의
        - 모든 함수에서 사용할 수 있는 지역 변수
        - 함수에 인수를 n개 넘겨서 호출하면 인수 값이 arguments에 저장
            - 예시
                
                ```jsx
                arguments[0] // 첫번째 인수 값
                arguments[1] // 두번째 인수 값
                arguments[2] // 세번째 인수 값
                ```
                
    - 특징
        - 프로퍼티로 length와 callee를 가짐
            - 예시
                
                ```jsx
                argument.length // 인수 개수
                arguments.callee // 현재 실행되고 있는 함수의 참조
                ```
                
        - arguments[i]의 값을 바ㅏ꾸면 i + 1번째 인자가 있을 때 그 값이 함께 바뀜
            - 예시
                
                ```jsx
                function f(x, y){
                	arguments[1] = 3;
                	console.log("x = " + x + ", y = " + y);
                }
                f(1, 2); // x = 1, y = 3
                ```
                
    - 활용
        - 인수 개수가 일정하지 않은 가변 인수 함수 정의 가능
            - 예시
                
                ```jsx
                function myConcat(separaotr){
                	var s = "";
                	for(var i=1; i<arguments.length; i++){
                		s += arguments[i];
                		if(i < arguments.length - 1) s += separator;
                	}
                	return s;
                }
                console.log(myConcat("/", "apple", "orange", "peach"));
                ```