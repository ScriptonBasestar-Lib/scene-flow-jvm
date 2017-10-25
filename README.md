# scene-flow-jvm

Scene을 연결하는 라이브러리 DSL을 지원하도록

이름은 고민중.
global-service-flow (GSF)

# 목표

* GroovyDSL
* 상태State 기억 - Cookie,Session,RequestParam이용 상태 저장
* State Store - 저장소 연결 인터페이스(DB, redis)
* 중간부터 진입 - 가끔 필요하지 않을까?? 이건 아님말고
* Form-Post방식 화면전환 - FlowId를 사용하면 각 Scene별로 주소를 지정해줘도 될 것 같다.

# 설계

## Scene 구조

각각의 분기를 모두 Scene이라고 한다.

<pre>
View : 화면이 있는 경우
Action : 행위만 있는 경우
Decision : YES/NO 상황 
</pre>

```
interface Scene;
View impl Scene;
Action impl Scene;
Decision impl Scene;
```

## DSL 구조

계획만.

회원가입Signup Flow
```
sceneView("start"){
  page("signup/root.tiles")
  handler(org.scriptonbasestar.signup.SignupService.init())
  link{
    (action="signup-button", to="check-validate")
  }
}

sceneDecision("check-validate"){
  handler(org.scriptonbasestar.signup.SignupService.checkValidate())
  link{
    (false, to="start")
    (true, to="add")
  }
}

sceneAction("add"){
  handler(org.scriptonbasestar.signup.SignupService.add())
  link{
    (exception="SBSignupException.class", to="fail")
    (to="success")
  }
}

sceneDecision("fail"){
  page("signup/fail.tiles")
  link{
    to(action="retry", to="start")
  }
}

sceneAction("success"){
  link{
    to("redirect:/mypage")
  }
}
```

