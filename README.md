#jquery-action


## 소개
* 언어 : JavaScript
* 필수 라이브러리 : jQuery 1.3.2 이상
* 블로그 포스트 : http://syaku.tistory.com/234
* 하위 버전 : https://code.google.com/p/jquery-action
* 하위 버전 메뉴얼 : https://docs.google.com/Doc?docid=0AWNiF48pXz7hZGZrN3hwejRfMTlrd2ttczVkYw&hl=ko

jQuery Action (이하 액션) 은 웹프로그램(혹은 HTML)에서 주기적으로 사용되는 자바스크립트 함수들을 모아 재사용이 용이하게 라이브러리화한 자바스크립트 프로그램이며, jQuery 기반으로 개발된 플러그인입니다.

액션은 ajax 와 submit 전송 방식을 지원하며, 폼 데이터를 전송하기 전에 해야할 일련의 작업들을 다양한 시나리오로 구성하여  제어할 수 있는 폼 데이터 전송 컨트롤러 프레임워크입니다.
> 파일 첨부(전송)는 지원하지 않습니다.

액션은 jQuery 에 의존하므로 jQuery 1.3.2 이상 라이브러리가 필요하며, 이하버전에서도 가능하나 보장할 수 없습니다.


##액션은 아래와 같은 기능을 제공합니다.

**1) 데이터 필터링**

* 데이터 입력 값 존재 검사 : 값을 입력 , 선택 , 체크 하였는 가를 체크함.
* 데이터 입력 값의 형태 검사 : 값이 숫자 , 영문 , 한글 , 한영조합 등등 인가를 체크함.
* 데이터 입력 값의 길이 검사 : 입력한 글자 수를 체크함.
* 데이터 입력 값의 비교 : 두개의 입력 값이 같은지 체크함.
* 데이터 선택 수 검사 : 라디오 및 체크 박스의 선택 수를 체크함.
* 데이터 정규표현식 검사 : 정규표현식을 이용하여 데이터 값 체크. 주로 이메일, 주민등록번호, 홈페이지 등등 정규표현식을 이용하여 입력한 값이 패턴과 일치한지를 체크함. 정규표현식을 추가하여 임의적인 체크가 가능함.


**2) 상황에 맞는 메세지 출력**

* 검사 과정에서 부합하지 않을 경우 그에 맞는 메세지를 출력함. (alert 혹은 커스텀)
* 모든 작업이 완료되고 전송 여부를 묻는 메세지를 출력함. (confirm 혹은 커스텀)
* 모든 메세지는 직접 만든 메세지를 출력하는 기능도 제공함.


**3) 메세지 국제화**
* 메세지 소스는 분리되어 있어 나라별로 국제화된 메세지를 출력할 수 있습니다. 
* 현재는 jquery.action-ko.js 대한민국 언어만 제공되고 있습니다.


**4) 자료변경**
* 폼을 전송하기 전에는 폼 내의 자료를 임의적으로 변경하거나 삭제할 수 있습니다.
* form 속성과 input,select 등의 입력 상자의 값을 변경할 수 있습니다.
* 폼 속성 제어는 하나의 폼으로 다양한 경로에 데이터를 전송할 때 유용합니다.


**5) 롤백**
* 액션이 진행되는 과정에 종료되었을 때, 변경된 자료들을 모두 원래데로 돌려놓습니다.
* form 속성, input,select 등의 입력상자의 값이 변경된 것을 모두 원래대로 되돌려 놓습니다.
* 롤백이 되지 않으면 다음 작업 진행에 문제가 될 수 있습니다.


**6) 전송 후 결과를 이용한 상황 처리**
* ajax 방식으로 폼 데이터를 전송하고 결과를 xml 형식으로 돌려받으면 액션에서 제시하는 xml 양식에 따라 상황을 처리할 수 있습니다.
* 전송 후 특정페이지로 이동 이벤트를 구현할 수 있으며, 직접 콜백 함수를 만들어 원하는 이벤트를 구현할 수 있습니다.
* 상황에 맞는 시나리오를 자유롭게 구성할 수 있습니다.


**7) 전송 전 인터셉터를 이용한 상황 처리**
* 액션이 실행되기 전, 전송되기 전, 전송된 후 성공인 경우, 전성된 후 등의 경우를 처리할 수 있게 각 함수를 제공하고 있으며, 개발자가 임의적인 작업을 수행할 수 있게 됩니다. return false; 인 경우 진행되는 액션은 종료되게 됩니다.

**8) 그외 기능**
* 액션은 자체적으로 공통(코어) 함수를 제공하고 있어, 반복적으로 사용되는 함수들을 사용할 수 있습니다.
* 그외 플러그인 들도 제공하고 있습니다. 레이어 출력, 팝업 출력 등등...


### 초기 설정

```html
<script type="text/javascript" language="javascript" src="http://code.jquery.com/jquery-1.6.2.min.js"></script>
<script type="text/javascript" language="javascript" src="./jquery.action.js"></script>
<script type="text/javascript" language="javascript" src="./jquery.action-ko.js"></script>
<link rel="stylesheet" type="text/css"  href="./jquery.action.css" />
```

### 옵션 설면

* 필수 옵션 : 없음
* 옵션 함수 호출 순서 : prepare , beforeAction, beforeSend, afterSend, ajaxComplete, redirect

```javascript
  send : 'ajax' // 폼 전송 방식 ajax | submit
, formAttr : null // 폼 속성 변경할 경우 ex) action=index.html&method=get
, filter : null // (json) 입력 상자 필터 정의
, values : null // (string) input,select 등 입력 박스 값을 임의적으로 변경할 때 사용. ex) user_id=admin&title=가가
, direct : null // (string) 폼 데이터를 전송하지 않고 direct 값만 전송할 경우 사용 ex) mod=insert&idx=1 (ajax 인경우만 가능)
, param : null // (string) ajax 폼 데이터 전송할때 추가되어 함께 전송됨. (ajax 인경우만 가능)
, prepare : null // (funciton) 액션이 실행되기 전에 초기작업 설정
, beforeAction : null // (function) 액션 함수 최초에 호출됨.
, beforeSend : null // (function) 폼 데이터 전송 전 호출됨.
, afterSend : null // (function) ajax 전송 후 오류가 없을 경우(error = false) 호출됨. ajax 전송인 경우에만 사용 가능
, ajaxComplete : null // (function) ajax 완료 후 호출됨. ajax 전송인 경우에만 사용 가능
, redirect : null // (string) ajax 전송 후 페이지 이동 ex) index.php?test=mode 
, ask : '' // "confirm alert" 이 출려될때 사용될 xml 참조한 메세지 (ask_msg 와 같이 사용할 수 없음) jquery.action-ko.js 파일의 message 참조하여 출력
, ask_msg : '' // "confirm alert" 이 출력될때 사용될 임의적인 메세지 (ask 와 같이 사용할 수 없음) 변수 값 그대로 출력
, loading : true // ajax 전송 시 로딩화면 출력 여부
, loading_mode : '' // 로딩화면 위치 center | customer
, loading_target : null // 로딩화면을 표시할 id 엘리먼트 없을 경우 기본 로딩화면을 출력함.
, setAjax : { } // jQuery ajax 옵션 설정
```

### 액션 기본 사용 예제

\#form 데이터를 ajax 방식으로 전송합니다.

```javascript
function onSubmit() {
  jQuery('#form').jaAction({ 
    params : 'page=12', // ajax 전송에서만 사용가능하며, 전송할때 해당 파라메터도 함께 전송함.
    ask_msg : '전송하시겠습니까?', // confirm 메세지 출력을 임의적으로 할 수 있음.
    
    beforeSend : function() { // 전송하기전에 호출됨.
      alert('전송합니다.');
    },
    afterSend : function() { // ajax 전송에서만 사용이 가능하며, 결과값 error 가 false 인 경우에만 실행됨.
      location.reload();
    }

  });
}
```

```html
<form id="form" method="post">
<input type="text" id="test" value="" />
<input type="button" value="저장1" onclick="onSubmit();" />
</form>
```

### 액션 필터링을 사용한 예제


```javascript
function onSubmit() {
  jQuery('#form_input').jaAction({ 
      values : 'mod=update' // mod 인풋박스의 값을 update 변경함.
    , formAttr : 'action=./save.html' // form 속성의 action 을 ./save.html 변경함.
    , send : 'submit' // form 을 submit 으로 전송함.
    , filter : [
        // #user_id 의 값이 없거나, user_id 형식의 값이 아니고 입력길이가 2자이상 4자이하가 아닌경우 아이디 .... 메세지 alert 창을 출력함.
        { target : "#user_id", params : "&filter=notnull&filter=user_id&length=2,4&title=아이디" }
        // #name 최대길이 10자이상을 넘을 경우 성명 .... 메세지 alert 창을 출력합니다.
      , { target : "#name", params : "&filter=notnull&max_length=10&title=성명" }
      , { target : "#pwd", params : "&filter=notnull&max_length=40&title=비밀번호" }
        // #pwd2 가 #pwd 의 값과 다를 경우 비밀번호 확인 .... 메세지 alert 창을 출력합니다.
      , { target : "#pwd2", params : "&filter=notnull&max_length=40&#pwd=!#pwd2&title=비밀번호 확인" }
      , { target : "#email", params : "&filter=email&title=메일" }
      // #age 의 값이 숫자가 아니거나, 50이상으로 입력한 경우 나이 ... 메세지 alert 창을 출력합니다.
      , { target : "#age", params : "&filter=notnull&filter=number&num=50&title=나이" }
      , { target : "#job", params : "&filter=notnull&title=직업" }
      // input:radio:[name=sex] 의 라디오박스 선택수가 0개인 경우 성별 ... 메세지 alert 창을 출력합니다.
      , { target : "input:radio:[name=sex]", params : "&selected=1&title=성별" }
      // input:radio:[name=s] 의 체크박스 선택수가 2개이상 3개이하가 아닌 경우 취미 ... 메세지 alert 창을 출력합니다.
      , { target : "input:checkbox:[name=s]", params : "&selected=2,3&title=취미" }

    ]
    , ask : 'update' // confirm 메세지 출력
    , beforeAction : function() { 
      // jaAction 메서드가 실행되기 전에 beforeAction 함수를 실행함. return false; 인 경우 jaAction 종료함.
      var ja = $.jaFilter._filtering(jQuery('input:radio:[name=is]'),'&selected=1&value=1');
      if (ja.error) { alert("동의를 선택하세요."); return false;} 
    }

  });
}
```

```html
<form id="form_input" method="post" action="">
hidden box : <input type="text" id="mod" name="mod" value="insert" />

<table border="1">
  <tr>
    <td colspan="2"><input type="button" value="저장" onclick="onSubmit();" /></td>
  </tr>
  <tr>
    <th>아이디</th>
    <td><input type="text" id="user_id" name="user_id" /></td>
  </tr>
  <tr>
    <th>이름</th>
    <td><input type="text" id="name" name="name" /></td>
  </tr>
  <tr>
    <th>비밀번호</th>
    <td><input type="text" id="pwd" name="pwd" /></td>
  </tr>
  <tr>
    <th>비밀번호 확인</th>
    <td><input type="text" id="pwd2" name="pwd2" /></td>
  </tr>
  <tr>
    <th>메일주소</th>
    <td><input type="text" id="email" name="email" /></td>
  </tr>
  <tr>
    <th>나이</th>
    <td><input type="text" id="age" name="age" /></td>
  </tr>
  <tr>
    <th>직업</th>
    <td>
      <select name="job" id="job">
        <option value="">선택</option>
        <option value="학생">학생</option>
        <option value="회사원">회사원</option>
        <option value="공무원">공무원</option>
      </select>

    </td>
  </tr>
  <tr>
    <th>성별</th>
    <td>
      <input type="radio" id="sex_boy" name="sex" /> 남
      <input type="radio" id="sex_girl" name="sex" /> 여
    </td>
  </tr>
  <tr>
    <th>취미</th>
    <td>
      <input type="button" value="모두선택" onclick="jQuery.ja.checked('#form_input input:checkbox:[name=s]');" />
      <input type="checkbox" id="s1" name="s" /> 여행
      <input type="checkbox" id="s2" name="s" /> 공부
      <input type="checkbox" id="s3" name="s" /> 컴퓨터
      <input type="checkbox" id="s4" name="s" /> 연애
      <input type="checkbox" id="s5" name="s" /> 독서
      <input type="checkbox" id="s6" name="s" /> 게임
    </td>
  </tr>
  <tr>
    <th>동의</th>
    <td>
      <input type="radio" id="is1" name="is" value="1" /> 동의
      <input type="radio" id="is_ss" name="is" value="2" /> 동의안함
      <input type="radio" id="is3" name="is" value="3" /> 모르겠음
    </td>
  </tr>
</table>
</form>
```


