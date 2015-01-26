## 컴포넌트에서 제공하는 기능 
  * 마우스 제스처 컴포넌트(mouseGestureDetector)는 화면에서 유저가 발생시키는 마우스 제스처를 분석하여 사용자 이벤트를 판단한다.
  * 컴포넌트에서 판단하는 이벤트 제스처의 종류는 다음과 같다.
    * 클릭(탭)
    * 더블클릭 
    * 롱탭 
    * 드래그
    * 플리킹, 스크롤 
  * 컴포넌트를 사용하기 위해서는 컴포넌트 생성시 설정값이 필요하다. (설정값에 대한 자세한 설명은 아래 항목을 참조한다) 

## 마우스 제스처 컴포넌트 생성시 설정값

| 필수여부 | 항목이름          |설명|기본값|
| ---------- | ----------- |----------- |----------- |
| 필수  | targetElement |마우스 제스처 컴포넌트를 적용할 영역.| |
| 필수  | callback     |마우스 제스처 결과 객체를 받아올 콜백함수. 여기서 정의한 콜백함수의 첫번째 파라미터로 제스처 결과 객체를 보낸다.| |
| | clickDistance | mousedown~mouseup 사이의 거리. clickDistance로 정의한 클릭 간격 거리가 이 설정값 이내에 있으면 더블클릭으로 정의한다. | 10px |
| | longTabTime | 롱탭을 정의하는 timeLimit. 이 값보다 더 길게 클릭되면 롱탭이다. | 200(ms) |
| | debugMode | 컴포넌트의 디버깅을 위한 옵션. true로 설정하면 컴포넌트 내부에서 출력하는 디버그 로그를 참조할 수 있다. | false |
| 필수 | flickScroll| 플리킹,스크롤에 대한 액션을 정의하는 객체. 상세 옵션 설명은 아래와 같다. <br><br> - availability :플리킹,스크롤 구분 여부. 이 값이 true로 설정되어 있는 경우에만 mouseUp시점에서 플리킹인지 스크롤인지 판단한다. (기본값 : true) <br>- timeLimit : drag가 이 설정값보다 길게 이루어졌을 경우 플리킹,스크롤을 구분하지 않고 drag처리한다. (기본값 : 800(ms)) <br>- measureType : 플리킹과 스크롤을 구분하는 타입. 'degree'와 'distance'두 값중 하나를 선택할 수 있다.(기본값 :'degree')<br> 1)'degree' : 플리킹,스크롤을 mousedown지점과 mouseup지점 사이의 각도로 판단한다. <br> 2)'distance' : 플리킹,스크롤을 일정 거리(단위:px)안에서의 움직임으로 판단한다. measureType을 'distance'로 설정하는 경우 measureValue값도 같이 설정해야 한다. <br> - measureType : flickScroll.measureType이 'distance'일 경우 설정해야 하는 두 지점 사이의 거리(단위:px) | |

## 설정값에 따른 제스처 판단 예제 
```
<script type="text/javascript" src="js/MouseGestureDetector.js"></script>
 
<script>
var printCallback= function(obj) {
    //컴포넌트로부터 받아온 정보(obj)를 가지고 로직 처리하는 부분
    console.log(obj.eventType);  
};
var obj = new ne.component.MouseGesture({
        'targetElement' : $("#test-area"),
        'longTabTime': 300,           
        'clickDistance': 10,
        'flickScroll': {
            'availability': true,      
            'timeLimit': 800,
            'measureType': 'degree'
        },
        'callback' : printCallback
});
</script>
```