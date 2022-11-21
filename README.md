# Hyperledger_Fabric_practice

## Hyperledger Fabric Network App 구성하기 위한 준비물

### BlockChain Network

- cryptogen
  - 인증 파일, 키파일 생성
  - crypto-config.yaml 파일에 명시되어 있는 내용을 사용
    - peer, orderer 등 명시되어 있음
- configtxgen
  - 전체적인 네트워크의 구조를 담고 있는 설정파일
    - genesis block 생성
    - channel TX
    - anchor peer TX
      - 각 organization에 속한 peer들이 다른 organization에 속해있는 peer들과 상호작용하기 위한 peer

- 버전에 따른 디렉토리 구조
  - 1.4
    - crypto-config
      - 인증 파일들이 들어
    - config
      - 네트워크 상호작용하는 파일
  - 2.2
- Docker
  - Docker compose를 통해 여러 환경을 한번에 관리해준다.
    - peer
    - orderer
    - couch DB
    - CA

### Chain code(Smart Contract)

- go 언어를 사용해 체인코드 작성
- 배포 및 instance화 진행
  - cli를 통해 배포
    - 1.4
      - 채인코드를 사용할 peer들에게 체인코드 설치
      - 채널에 설치한 후 사용가능하도록 instance화 진행
    - 2.2
- 테스트
  - query
    - 조회(트랜잭션을 발생시키지 않음)
  - inoke
    - 수정(트랜잭션을 발생시킴)

### Application

- 웹서비스
  - Server
  - Client
- 보통 Server에서 체인코드를 연결한다.
- SDK를 이용
  - fabric-network
    - 트랜잭션 및 데이터를 조회할 수 있는 메서드 제공
      - evaluate TX(query에 해당)
      - submit TX(invoke에 해당)
    - wallet
      - 인증된 사용자만이 사용할 수 있도록 키, 인증서 관련된 것들을 만들어 wallet에 저장한다.
      - 기본적으로 file system에 저장
      - 메모리, couch db에 저장하기도 함
    - gateway 제공
      - 실질적으로 애플리케이션과 네트워크를 연결해주는 중간다리 역할
  - fabric-ca-client
    - ca의 역할을 수행할수 있는 메서드 제공
      - identity 파일 생성
        - admin
        - user