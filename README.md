# http://badamap.com/
# http://bogol.duckdns.org/ 
# https://Bogol-E.github.io/badamap (Fake)
> - [ ] 마커
>> - [x] 대한민국 좌표 범위 제한, 줌레벨 제한, 기본 뷰 설정
>> - [x] 좌표 위치 SVG 마커 표시
>> - [x] 로테이션, 속도 에니메이션
>> - [x] 줌레벨 연동 에니메이션 제어, 선박명 블라인드
>> - [x] DB서버 웹소켓 연결
>> - [x] 속성에 따른 svg 옵션
>> - [ ] SSE연결, 서버시간 기준 좌표 동기화
>> - [ ] 상태별 splits 생명주기 관리 촤적화
> - [ ] 온레이어 팝업
>> - [ ] 배이름, mmsi 검색
>> - [ ] 마커 클릭 과거 경로 추적
>> - [ ] 마커 고정 지도 로테이션 네비게이션모드
>> - [ ] 상세 정보 출입항기록 등 openapi 파싱
>> - [ ] 해로드 레이어 교체
>> - [ ] 전체화면, 클라이언트 gps 버튼
>> - [ ] 선박별 즐겨찾기 저장
>> - [ ] 지도 뷰포인트 저장
>> - [ ] 운항 일지 저장
>> - [ ] 예측모델 flask api 적용
>> - [ ] UI/UX 튜토리얼
> - [ ] 로그인 구현
>> - [ ] Oauth 인증
>> - [x] 리눅스 - NginX - Postgresql - Node 구축
>> - [x] 서버 연결, cros
>> - [ ] 웹 애플리케이션 방화벽(WAF)
>> - [ ] Anti XSS & SQL Injection & Cross-Site Scripting
>> - [ ] 클라이언트 요청을 제한 디도스(DDoS) 공격을 완화
>> - [ ] 특정 국가 또는 지역의 IP 주소 범위를 차단
>> - [ ] 게시판 생성. 운항일지 사진등 공유 기능
>> - [ ] ssl 인증
>> - [ ] Docker 패키징, 배포

```
 npx rollup -c --bundleConfigAsCjs rollup.config.js
```
## HTTPS 사용을 위한 테스트 SSL 인증서 발급
### 환경 : window10, openssl 환경변수 설정
```
openssl 인증서 발급
private.key 이름의 개인키 발급
openssl genpkey -algorithm RSA -out private.key
public.key 이름의 공개키 발급
rsa -in private.key -pubout -out public.key
CA인증을 대체하기 위해 자체 CA인증을 진행한다.
openssl genpkey -algorithm RSA -out rootCA.key
openssl req -new -key rootCA.key -out rootCA.csr
openssl x509 -req -days 365 -in rootCA.csr -signkey rootCA.key -out rootCA.crt
스프링부트에서 사용하기 위해 p12 키스토어로 인코딩한다.
keytool -genkeypair -alias myapp -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore keystore.p12 -validity 3650
스프링부트 application.properties
server.port = 8080
server.ssl.key-store-type=PKCS12
server.ssl.key-store=c:/certs/keystore.p12 //경로 입력에 유의한다.
server.ssl.key-store-password=123456
```