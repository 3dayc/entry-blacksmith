# Entry_Blacksmith

### Entry_Blacksmith issue modification

[엔트리개발 v1.9.1 + 20191211]
#목적
대장장이보드와 안드로이드 앱 : 블루투스 블록 수정 

#범위
; 대장장이보드 블루투스 블록
1. [ entry-hw > blacksmith.js ]
2. [ entryjs > block_blacksmith.js ]

#내용
1. 수신이 전혀 안되던 부분 수정
 -수신데이터 형변환과정에서 오류확인.
 -값을 숫자와 문자로 구분하던 부분 삭제.
 -제한없이 입력값 그대로 수신.
   ex) "1235" "efje" "kkk345"
 -블록명세코드 변경 
   '블루투스 RX 2 핀 %1 데이터 값' -> '블루투스 RX 2 핀 데이터 값'
2. 통신이 하드웨어 최초연결시에만 잘되던 문제 해결.(엔트리hw 종료 전까지)
 - sendQeue의 'GET' 값 중복체크부분(isRecentData)이 초기화에 이슈를 발생시킴.
 -'SET'과 동일한 구조로 만드는과정에서의 이전 개발자 실수로 판단됨.
 -해당부분 삭제

#발생이슈
1. "entry-hw 모듈 종속성 에러" 
 -> package.json, package_lock.json, Node_Module 제거 후 
      npm install  | npx electron-rebuild
2. 블루투스 앱 모두 같은 결과가 나오는게 아님.
  1) "BT Chat" : 아두이노와 송수신 가능/ 디버깅 및 로그확인용으로 좋음
  2) "BlueTooth Serial Controller" : 반응형 인터페이스로 컨트롤러 최적
  3) "Arduino bluetooth controller" : 다양한 기능 활용가능하지만 통신 정확도 신뢰성 부족 

관련 테스트는 개발과정에서 체크하는 부분과,
수요일 저녁에 팀원과 함께 진행합니다.

이후 목요일에 엔트리에 PR합니다.

코드변경내용은 사진첨부하겠습니다.
