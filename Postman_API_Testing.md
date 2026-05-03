Postman_API_Testing<br>
---------------------------------------------------------------------------
Postman과 Newman, CronTab 세팅을 통한 API 자동화 구현<br>

용도: dev/prod API TEST 및 테스트 보고서 자동화<br>
Jsonplaceholder의 mock api를 기반으로 작성
<br>
<br>
<img width="985" height="517" alt="스크린샷 2026-05-03 오후 2 40 39" src="https://github.com/user-attachments/assets/2c89fa21-111e-4c4e-b523-df922f3ca28b" />
자동화 할 api test 목록을 json 파일로 export 함 
<br>
<br>
<img width="854" height="462" alt="스크린샷 2026-05-03 오후 2 41 51" src="https://github.com/user-attachments/assets/dd98ba79-38e7-4878-a1e1-6596daa9c26c" />
터미널에서 newman 명령을 실행하면 postman과 동일하게 json 형태의 api를 조회함 (REST API)
<br>
<br>
<img width="1112" height="744" alt="스크린샷 2026-05-03 오후 2 43 17" src="https://github.com/user-attachments/assets/eba9b2a1-d2f9-4128-8bcc-21466128e86f" />
이후 보고서 형식의 newman 파일 생성

<img width="1073" height="328" alt="스크린샷 2026-05-03 오후 3 06 20" src="https://github.com/user-attachments/assets/d6fbed02-4100-4c4f-b641-91899b985d69" />
만약 실패한 경우 Failed Tests 탭에서 실패 원인 확인할 수 있음(400/404/500 그 외)
<br>
<br>
<img width="583" height="108" alt="스크린샷 2026-05-03 오후 2 44 36" src="https://github.com/user-attachments/assets/16001c11-f931-4b7b-acfb-2bd784494b78" />
크론탭에서 api test 하고 싶은 날(e.g. 월~금 영업일) 설정해두면 특정 요일 및 시간에 자동으로 테스트가 실행, 보고서 발행 됨
<br>
<br>
<img width="985" height="356" alt="스크린샷 2026-05-03 오후 2 46 04" src="https://github.com/user-attachments/assets/91d1fb39-bf8e-4d50-82ab-507cad9aea4d" />
슬랙 webhook 연동을 통해 테스트 성공/실패 유무를 채널로 받아 볼 수도 있음


<img width="428" height="110" alt="스크린샷 2026-05-03 오후 3 28 11" src="https://github.com/user-attachments/assets/75d9d48f-2435-405e-81a8-d0c916943e9c" />
모든 api test가 200/201로 떨어진 경우(성공)
<br>
<br>
<img width="465" height="97" alt="스크린샷 2026-05-03 오후 3 28 04" src="https://github.com/user-attachments/assets/caa5993e-915a-4bb3-858e-f71e2da04e94" />
1개 이상의 api test에서 200/201 외의 값이 있는 경우(실패)
