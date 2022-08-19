## MVC 패턴

Model(객체) + View(출력) + Controll(처리)를 합쳐 일컫는다.

**과정**

클라이언트의 요청 ➡ Dispatcherservlet이 입력/변환 처리를 하고 모델(결과를 저장할 객체)를 만들어 처리에 전달 ➡ 처리에서는 Controller가 처리해서 결과를 Model에 저장 ➡ 입력(Model)은 출력에 전달 ➡ 출력(view)가 응답 ➡ 클라이언트에게 전달