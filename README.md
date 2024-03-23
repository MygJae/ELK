# ELK
우분투18.04, 자바11, ElasticSearch, Kibana, Logstash, filebeat 7.17.18
## 01. 윈도우10에서 우분투 설치
### WSL 활용하기(윈도우 버전 체크 필요)
#### 1. 제어판 -> Windows 기능 켜기/끄기 -> Linux용 Windows 하위 시스템 체크, 가상 머신 플랫폼 체크 -> 재부팅
#### 2. 파워쉘 실행 -> ```wsl --set-default-version 2``` -> WSL 2와의 주요 차이점... 문구시 완료
#### 3. 시작화면 -> MS Store -> Ubuntu -> 다운로드 -> 실행 -> ```explorer.exe .``` 윈도우에서 폴더 실행 됨(docker, vscod 사용 가능)

## 02. ELK 환경 구성
### JDK, ELK 설치
#### 1. https://www.elastic.co/kr/support/matrix#matrix_os 설치 파일 지원 OS버전 확인
#### 2. 우분투 실행 -> ```sudo apt update && sudo apt upgrade``` -> ```sudo apt install default-jdk``` -> ```java --version``` -> 자바 기반이므로 JDK설치 필요
#### 3. elastic.co/kr/downloads/elasticsearch -> DEB X86 64 선택, 파일링크 복사 -> ```wget [파일경로]``` -> ```sudo dpkg -i [파일이름]``` -> 나머지도 이 방식으로 설치
#### 4. 인스톨 경로: /usr/share/elasticsearch -> config 경로: /etc/elasticsearch -> 정상 설치 확인
#### 5. ```sudo service elasticsearch start/status/stop``` 실행 -> 쉘파일 생성 및 권한부여 el_start.sh
#### 6. ```curl -X GET localhost:9200, 5601, 5044 ``` 정상 확인 -> (52)Empty reply from server ->  https필요, 7버전으로 다운그레이
#### 7. 외부 접속 ```vim /etc/elasticsearch/elasticsearch.yml``` -> i를 입력하여 수정상태로 바꾸고 Network로 이동하여 network.host: 0.0.0.0 변경, 포트 변경

## 03. 운영
### ELK 플로우
#### 1. Filebeat 각 서버에 설치 -> 로그 파일 수집 -> Logstash로 Input Output 하기 , tags를 이용해서 구분
#### 2. Logstash 필터링 ->  tags로 필터링이랑 인덱스 설정해서 ElasticSearch로 보내기
#### 3. ElasticSearch 데이터 적재 -> 인덱스 패턴 생성
#### 4. Kibana 데이터 시각화

## 04. Tip
#### 리눅스 권한 필요: etc/kibana/ -> 권한 부여 해야 list 보임 -> kibana.yml 권한 부여 -> 수정
