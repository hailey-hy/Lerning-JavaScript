### 1. 이벤트 처리기

- 정의
    
    <aside>
    💡 이벤트가 발생했을 때 실행되는 함수
    
    </aside>
    
    - 이벤트: 사용자가 버튼을 클릭하는 행위처럼, 단말기와 애플리케이션이 처리할 수 있는 동작이나 사건
    - 이벤트 주도형 프로그램: 이벤트가 발생할 때까지 기다렸다가 이벤트가 발생했을 때 미리 등록해 둔 작업을 수행하는 프로그램
- 주요 이벤트 처리기 이름
    
    
    | 이벤트 처리기 이름 | 이벤트 종류 |
    | --- | --- |
    | onclick | 마우스로 클릭했을 때 |
    | onmouseover | 마우스가 포인터가 HTML 요소 위에 놓여 있을 떄 |
    | onkeydown | 키보드 키를 눌렀을 때 |
    | onchange | input 요소의 값이 바뀌었을 때 |
    | onsubmit | 폼 제출 버튼을 눌렀을 때 |

### 2. HTML 요소 속성에 이벤트 처리기 등록하기

- 예시
    
    ```html
    <!DOCTYPE html>
    <html>
    <head>
    <meta charset="UTF-8">
    <title>Insert title here</title>
    </head>
    <script>
    	function displayTime(){
    		var d = new Date();
    		console.log("현재 시각은 " + d.toLocaleString() + "입니다.");
    	}
    </script>
    <body>
    	<input type="button" value="click" onclick="displayTime()">
    </body>
    </html>
    ```
    

### 3.  DOM에서 가져온 HTML 요소에 이벤트 처리기 지정하기

- DOM이란
    - DOM: 자바스크립트 등이 HTML 요소를 조작할 수 있게 하는 인터페이스
    - DOM 객체: window, document 등
- 등록 방법
    1. wondow.onload를 사용해 HTML 문서를 다 읽어들인 후 아래 실행
    2. document.getElementById 메서드를 사용해 특정 ID 속성 값을 가진 HTML 요소의 요소 객체를 가져옴
    3. 요소 객체의 이벤트 처리기 프로퍼티에 이벤트 처리기로 동작할 함수를 등록
- 예시
    
    ```html
    <!DOCTYPE html>
    <html>
    <head>
    <meta charset="UTF-8">
    <title>Insert title here</title>
    </head>
    <script>
    	function displayTime(){
    		var d = new Date();
    		console.log("현재 시각은 " + d.toLocaleString() + "입니다.");
    	}
    	
    	window.onload = function(){
    	//i. window 객체의 ONload 프로퍼티에 함수 저장
    	//웹 브라우저가 문서를 모두 읽어들인 후 실행
    	
    		var button = document.getElementById("button");
    		//ii. input 요소의 객체 가져오기
    		
    		button.onclick = displayTime;
    		//iii. input요소를 클릭했을 때 동작하는 이벤트 처리기 등록
    
    </script>
    <body>
    	<input type="button" value="click" onclick="displayTime()">
    </body>
    </html>
    ```
    
- 해석
    1. wondow.onload를 사용해 HTML 문서를 다 읽어들임
        - HTML과 자바스크립트 코드 분리를 위해 script 요소를 head의 자식 요소로 배치
            - DOM을 사용 시 body의 밖에서 body의 HTML 요소 동작 가능
            - 그러나, script 요소는 아직 body를 읽어들이기 전 실행됨
            - 따라서 이벤트 처리기 등록하는 작업의 실행 시점을 HTML 문서 전체를 읽어 들인 이후로 미룰 필요가 있음
                
                → window 객체의 onload 프로퍼티에 이벤트 처리기를 등록
                
    2. document.getElementById 메서드를 사용해 특정 ID 속성 값을 가진 HTML 요소의 요소 객체를 가져옴
        - document.getElementById 메서드는 전달받은 인수를 Id 속성의 값으로 가지고 있는 HTML 요소의 요소 객체를 반환
            - 찾지 못하면 null 반환
        - id 속성 값이 button인 요소의 요소 객체를 가져와 변수 button에 저장
    3. 이벤트 처리기 프로퍼티에 이벤트 처리기로 동작할 함수를 등록
        - input 요소를 클릭했을 때 동작할 이벤트 처리기 등록
        - 요소 객체의 onclick 프로퍼티 값으로 함수 displyTime의 참조를 대입

### 4. 이벤트 처리기 제거

- 이벤트 처리기가 등록되어 있지 않은 이벤트 처리기 프로퍼티에는 기본적으로 null이 담겨 있음
- 따라서 이벤트 처리기 제거를 위해서는 단순히 Null을 대입
- 예시
    
    ```jsx
    	button.onclick = null;
    ```
    

### 5. 타이머

1. setTimeout
    
    <aside>
    💡 일정 시간이 흐른 후 함수 실행
    
    </aside>
    
    - 동작 예시
        
        ```jsx
        setTimeout(function() {
        	console.log(new Date());
        }, 2000);
        ```
        
    - clearTimeout()
        - setTimeout()이 반환한 값을 인수로 넘기면 함수 실행이 취소됨
2. setInterval
    
    <aside>
    💡 일정한 시간 간격에 따라 반복해서 실행
    
    </aside>
    
    - 동작 예시
        
        ```jsx
        setinterval(function(){
        	console.log(new Date());
        }, 1000);
        ```