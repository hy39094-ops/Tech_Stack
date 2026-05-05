Android_Studio_SQL
------------------------------------
용도: UI상 데이터 중복 노출 발생 시 App Inspection 기능 사용<BR> 
로컬 DB 무결성 검증을 통한 이슈(클라/서버) 분리 및 Root Cause 분석 
<BR>
<BR>
실무 활용1: 관심그룹 내 <삼성전자> 종목이 2개가 노출되는 경우<BR>
SELECT COUNT(*) FROM Favorite_Group_Master <BR>
WHERE stock_name = '삼성전자';
<BR>
<BR>
Case 1: 쿼리 결과가 1개인 경우 (UI 중복)<BR>
판단: 로컬 DB의 데이터 정상. 이를 불러와서 화면에 뿌려주는 API 응답 중복 또는 클라이언트 렌더링 로직의 오류<BR>
결론: 서버 이슈 또는 클라이언트 이슈로 분류<BR>

Case 2: 쿼리 결과가 2개인 경우(DB 중복)<BR>
판단: 로컬 DB 자체에 동일한 종목 마스터가 중복 저장됨. 데이터 생성 과정에서 무결성이 깨졌다고 확인 할 수 있음<BR>
결론: 데이터베이스 무결성 이슈로 확인하여 서버(또는 시세) 이슈로 등록<BR>
<BR>
<BR>
<BR>
<BR>
<BR>
<BR>
실무 활용2: 관심그룹 내 종목편집을 실행하여 목록 순서를 변경하였지만, 목록 변경이 되지 않는 경우<BR>
SELECT stock_name, sort_order <BR>
FROM Interest_Group_Items <BR>
WHERE group_id = 'favorite_group'<BR> 
ORDER BY sort_order ASC;<BR>
<BR>
<BR>
Case 1: DB 내 sort_order 값은 정상적으로 변경된 경우<BR>
현상: SQL 결과에서는 사용자가 수정한 순서(0, 1, 2...)대로 데이터가 찍히지만, 앱 UI에서는 이전 순서로 보임.<BR>
판단: 로컬 DB 저장 로직은 정상이나, UI를 그려주는 클라이언트가 DB에서 데이터를 새로 불러오지(Fetch) 않거나 캐시된 데이터를 계속 보여주는 상태임.<BR>
결론: 클라이언트(Client) UI 렌더링 및 캐시 갱신 이슈로 분류.<BR>
<BR>
<BR>
Case 2: DB 내 sort_order 값이 이전 상태 그대로인 경우<BR>
현상: SQL 결과값이 사용자가 편집한 순서가 아닌, 예전 순서 그대로 저장되어 있음.<BR>
판단: 사용자의 편집 액션이 발생했을 때, 로컬 DB에 새로운 인덱스 값을 쓰는(Update) 로직이 실패했거나 DB 트랜잭션이 정상적으로 완료되지 않음.<BR>
결론: 로컬 데이터베이스(DB) 저장 로직 이슈로 분류. (동기화 실패 포함)<BR>
