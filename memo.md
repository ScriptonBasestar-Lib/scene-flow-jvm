보고지울 메모.

flow에서 일정 주소를 관리 할 필요가 있다.
ex) 회원가입 /signup/**

1. (GET)/signup 주소로 진입. 뒤에 뭐가 붙은건 다 무시
2. (GET)/signup/emailConfirm/request 에서 이메일 확인요청
3. (GET)/signup/emailConfirm/redirect?code=9090iio9090iooi 이메일에서 클릭해서 확인받기
4. ~~~~~~
5. (POST)/signup/finish 최종 버튼 클릭시 액션

이렇게 주소를 매핑해서 사용하려면 주소를 매핑하는 방식을 결정 할 필요가 있는데...

Spring의 HandlerMapping 을 구현해서 사용.
SceneFlowHandlermapping
