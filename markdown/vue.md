## 뷰 인스턴스

### 뷰 인스턴스의 정의와 속성

* 뷰 인스턴스는 뷰로 화면을 개발하기 위해 필수적으로 생성해야 하는 기본 단위다.

* 뷰 인스턴스 형식.

  ```js
  new Vue({
    ...
  });
  ```

* 뷰 인스턴스 생성.

  * 예제) Hello Vue 

  ```js
  <html>
    <head>
      <title>Vue Sample</title>
    </head>
    <body>
      <div id="app">
        {{ message }}
      </div>
      <script src ="https://cdn.jsdelivr.net/npm/vue@2.5.2/dist/vue.js"></script>
      <script>
        new Vue({
          el:'#app',
          data:{
            message:'Hello Vue.js!'
          }
        });
      </script>
    </body>
  </html>
  ```

* 뷰 인스턴스 생성자 

  Vue 생성자는 뷰 라이브러리를 로딩하고 나면 접근 할 수 있다.

* 뷰 인스턴스 옵션 속성

  뷰 인스턴스 옵션 속성은 인스턴스르 생성할 때 재정의할 data, el, template 등의 속성을 의미 한다.

  예를 들어, Hello Vue 예제에서는 data라는 미리 정의되어 있는 속성을 사용했다. 그 안에 message라는 새로운

  속성을 추가하고 Hello Vue.js! 라는 값을 주었을 뿐. el 속성 역시 미리 정의되어 있으며 뷰로 만든 화면이 그려지는 

  시작점을 의미한다. 뷰 인스턴스로 화면을 렌더링 할 때 화면이 그려질 위치의 돔 요소를 지정해 주어야 한다.

  ![인스턴스의 el속성](../img/1.jpeg)

  이 외에도 template, methods, created 등 미리 정의되어 있는 속성을 사용할 수 있다.

  | 속성     | 설명                                                         |
  | -------- | ------------------------------------------------------------ |
  | template | 화면에 표시할 HTML, CSS 등의 마크업 요소를 정의하는 속성, 뷰의 데이터 및 기타 속성<br />들도 함께 화면에 그릴 수 있다. |
  | methods  | 화면 로직 제어와 관계된 메서드를 정의하는 속성, 마우스 클릭 이벤트 처리와 같이 화면의<br />전반적인 이벤트와 화면 동작과 관련된 로직을 추가할 수 있다. |
  | created  | 뷰 인스턴스가 생성되자마자 실행할 로직을 정의할 수 있는 속성 |



* 뷰 인스턴스의 유효 범위

  뷰 인스턴스를 생성하면 HTML의 특정 범위 안에서만 옵션 속성들이 적용되어 나타난다.. 

  이를 인스턴스의 유효범위 라고 합니다. 인스턴스의 유효 범위는 el속성과 밀접한 관계가 있다.

  화면에 인스턴스 옵션 속성을 적용하는 과정은 다음과 같다.

  <img src="/Users/xxbro/bro-lab/vuejs/markdown/img/2.jpeg" alt="2" style="zoom:50%;" />

  <<샘플코드>>

  ```js
  new Vue({
    el : '#app',
    data : {
      message : 'Hello Vue.js!'
    }
  });
  ```

  인스턴스 옵션 속성 el과 data를 인스턴스에 정의하고 new Vue()로 인스턴스를 생성한다.

  그리고 브라우저에서 위 샘플코드를 실행하면 아래와 같이 el 속성에 지정한 화면요소(돔)에 인스턴스가 부착된다.

  <img src="/Users/xxbro/bro-lab/vuejs/markdown/img/3.jpeg" alt="3" style="zoom:50%;" />

  el 속성에 인스턴스가 부착되고 나면 인스턴스에 정의한 옵션 객체의 내용(data속성)이 el 속성에 지정한 화면요소와

  그 이하 레벨의 화면 요소에 적용되어 값이 치환된다.

  <img src="/Users/xxbro/bro-lab/vuejs/markdown/img/4.jpeg" alt="4" style="zoom:50%;" />

  data 속성의 message 값 Hello Vue.js! 가 {{ message }}와 치환된다.

  

* 인스턴스의 유효 범위 확인

  ```js
  <div id="app">
    
  </div>
  {{ message }}
  ```

  위 코드를 실행하면 결과는 아래 와 같다.

  <img src="/Users/xxbro/bro-lab/vuejs/markdown/img/5.jpeg" alt="5" style="zoom:50%;" />

  message 속성의 값이 Hello Vue.js! 로 바뀌지 않고 그대로 출력되는 이유는 인스턴스의 유효 범위 때문이다.

  <img src="/Users/xxbro/bro-lab/vuejs/markdown/img/6.jpeg" alt="6" style="zoom:50%;" />

  현재 코드에서 인스턴스의 유효 범위는 el 속성으로 지정한 <div =id="app"> 태그 아래에 오는 요소들로 제한된다.

  '<div>'태그 바깥에 있는 {{ message }} 는 뷰에서 인식하지 못하기 때문에 Hello Vue.js!로 바뀌지 않고 {{ message }}

  그대로 출력된다.

  

* 뷰 인스턴스 라이프 사이클

  * 인스턴스의 상태에 따라 호출할 수 있는 속성들을 라이프 사이클(life cycle) 속성이라고 한다.

  * 각 라이프 사이클 속성에서 실해되는 커스텀 로직을 라이프 사이클 훅(hook) 이라고 한다.

  * 라이프 사이클 속성에는 created, beforeCreate, beforeMount, mounted 등 인스턴스의 생성, 변경, 소멸과 

    관련되어 총 8개가 있다.

    <img src="/Users/xxbro/bro-lab/vuejs/markdown/img/7.jpeg" alt="7" style="zoom:50%;" />

    위 그림은 인스턴스가 생성되고 나서 화면에 부착된 후 소멸되기 까지의 전체적인 흐름을 나타낸 뷰 인스턴스 라이프

    사이클 다이어 그램 이다.

    뷰 인스턴스 라이프 사이클은 크게 4단계 로 이루어 진다.

    * 인스턴스의 생성
    * 생성된 인스턴스를 화면에 부착
    * 화면에 부착된 인스턴스의 내용이 갱신
    * 인스턴스가 제거되는 소멸

    부착 -> 갱신 구간은 데이터가 변경되는 경우에만 거치게 된다. 

    그리고 각 단계 사이에 라이프 사이클 속성 created, mounted, updated 등이 실행된다.

    

    * beforeCreate

      인스턴스가 생성되고 나서 가장 처음으로 실행되는 라이프 사이클 단계다.

      data 속성과 methods 속성이 아직 인스턴스에 정의되어 있지 않고, 돔과 같은 화면 요소에도 

      접근할 수 없다.

      

    * created

      beforeCreate 라이프 사이클 단계 다음에 실행되는 단계다.

      data 속성과 methods 속성이 정의 되었기 때문에 this.data 또는 this.fetchData()와 같은 로직들을 이용하여

      Data 속성과 methods 속성에 정의된 값에 접근하여 로직을 실행 할 수 있다. 다만, 아직 인스턴스가 화면 요소에

      부착되기 전이기 때문에 template 속성에 정의된 돔 요소로 접근할 수 없다.

      그리고 data 속성과 methods 속성에 접근할 수 있는 가장 첫 라이프 사이클 단계이자 컴포넌트가 생성되고 나서 

      실행되는 단계이기 때문에 서버에 데이터를 요청하여 받아오는 로직을 수행하기 좋다.
    
      
    
    * beforeMount
    
      created 단계 이후 template 속성에 지정한 마크업 속성을 render() 함수로 변환한 후 el 속성에 지정한 화면
    
      화면 요소(돔)에 인스턴스를 부착하기 전에 호출되는 단계 입니다. render() 함수가 호출됙 직전의 로직을 추가하기
    
      좋다. 
    
      ```
      render()는 자바스크립트로 화면의 돔을 그리는 함수.
      ```
    
      
    
    * mounted
    
      el 속성에서 지정한 화면 요소에 인스턴스가 부착되고 나면 호출되는 단계로, template 속성에 정의한 화면 요소
    
      (돔)에 접근할 수 있어 화면 요소를 제어하는 로직을 수행하기 좋은 단계다. 다만, 돔에 인스턴스가 부착되자마자
    
      바로 호출되기 때문에 하위 컴포넌트나 외부 라이브러리에 의해 추가된 화면 요소들이 최종 HTML 코드로 변환
    
      되는 시점과 다를 수 있다. 
    
      ```
      변환되는 시점이 다를 경우 $nextTick() API를 활용하여 HTML 코드로 최종 파싱(변환) 될 때까지 기다린 후 돔 제어 로직을 추가하자.
      ```
    
      
    
    * beforeUpdate
    
      el 속성에서 지정한 화면 요소에 인스턴스가 부착되고 나면 인스턴스에 정의한 속성들이 화면에 치환된다.
    
      치환된 값은 뷰의 반응성(Reactivity)을 제공하기 위해 $watch속성으로 감사한다. 이를 데이터 관찰이라 한다.
    
      ```
      뷰의 반응성
      => 뷰의 특징 중 하나로, 코드의 변화에 따라 화면이 반사적으로 반응하여 빠르게 화면을 갱신하는 것을 의미
      ```
    
      또한 beforeUpdate는 관찰하고 있는 데이터가 변경되면 가상 돔으로 화면을 다시 그리기 전에 호출되는 단계이
    
      며, 변경 예정인 새 데이터에 접근할 수 있어 변경 예정 데이터의 값과 관련된 로직을 미리 넣을 수 있다.
    
      여기에 변경하는 로직을 넣더라도 화면이 다시 그려지지는 않는다.
    
      
    
    * update
    
      데이터가 변경되고 나서 가상 돔으로 다시 화면을 그리고 나면 실해되는 단계.
    
      이 단계에서 데이터 값을 변경하면 무한 루프에 빠질 수 있기 때문에 값을 변경하려면 computed, watch와 
    
      같은 속성을 사용해야 한다. 따라서 데이터 값을 갱신하는 로직은 가급적이면 beforeUpdate에 추가하고,
    
      updated에서는 변경 데이터의 화면 요서(돔)와 관련된 로직을 추가하는 것이 좋다.
    
      ```
      mounted 단계와 마찬가지로 주입된 요소의 최종 변환 시점이 다를 수 있다 $nextTick()을 사용하여 변환이 완료될 때까지 기다렸다가 로직을 추가하자.
      ```
    
      
    
    * beforeDestroy
    
      뷰 인스턴스가 파괴되기 직전에 호출되는 단계. 아직 인스턴스에 접근할 수 있으며, 
    
      뷰 인스턴스의 데이터를 삭제하기 좋은 단계.
    
      
    
    * destroyed
    
      뷰 인스턴스가 파괴되고 나서 호출되는 단계. 
    
      뷰 인스턴스에 정의한 모든 속성이 제거되고 하위에 선언한 인스턴스들 또한 모두 파괴된다.
    
      
    
    * 라이프 사이클 실습 예제
    
      ```html
      <html>
        <head>
          <title>Vue Instance Lifecycle</title>
        </head>
        <body>
          <div id="app">
            {{ message }}
          </div>
      
          <script src="https://cdn.jsdelivr.net/npm/vue@2.5.2/dist/vue.js"></script>
          <script>
            new Vue({
              el: '#app',
              data:{
                message:'Hello Vue.js!'
              },
              beforeCreate:function(){
                console.log("beforeCreate");
              },
              created:function(){
                console.log("created");
              },
              mounted:function(){
              	console.log("mounted");
              },
              updated:function(){
              	console.log("updated");
              }
            });
          </script>
        </body>
      </html>
      ```
    
    * 실행결과
    
      ![8](/Users/xxbro/bro-lab/vuejs/markdown/img/8.png)
    
      도해의 흐름대로 beforeCreate, created, mounted가 표시되는 것을 확인할 수 있다.
    
      
    
    * message값을 변경한 라이프 사이클 실습 예제
    
      ```html
      <html>
        <head>
          <title>Vue Instance Lifecycle</title>
        </head>
        <body>
          <div id="app">
            {{ message }}
          </div>
      
          <script src="https://cdn.jsdelivr.net/npm/vue@2.5.2/dist/vue.js"></script>
          <script>
            new Vue({
              el: '#app',
              data:{
                message:'Hello Vue.js!'
              },
              beforeCreate:function(){
                console.log("beforeCreate");
              },
              created:function(){
                console.log("created");
              },
              mounted:function(){
              	console.log("mounted");
                this.message = '헬로우 뷰!';
              },
              updated:function(){
              	console.log("updated");
              }
            });
          </script>
        </body>
      </html>
      ```
    
    * 실행결과
    
      ![9](/Users/xxbro/bro-lab/vuejs/markdown/img/9.png)
    
    * mounted 단계에서 화면에 표시되는 message값이 갱신 되었고, 이에 따라 updated 로그가 출력 되었다.
    
      여기서 중요한 것은 인스턴스의 데이터가 갱신되면서 라이프 사이클 단계가 beforeUpdate, updated 단계로 
    
      진입했다는 점 이다. 
    
      이처럼 각 인스턴스 라이프 사이클에 맞춰 원하는 로직을 추가하여 원하는 시점에 실행할 수 있다.
    
      
  
  ## 뷰 컴포넌트
  
  
  
  

