# MSA  


## 통신 패턴

- MSA 설계를 통해 도출된 서비스 간 어떤 방식으로 통신을 할 지 결정하는 패턴

- Sync Pattern(동기)
  - 어떤 서비스가 다른 서비스로 특정 Request 이후 그 Response 를 받을때 까지 멈춰있어도 되는 경우
  - e.g. HTTP(Restful), gRPC
- Async Pattern(비동기)
  - 어떤 서비스가 다른 서비스로 특정 Request 이후, 그 Response를 당장은 받지 않아도 되는 경우
  - e.g. Kafka 등을 이용한 Message Queueing, Callback(응답을 받을때 Event Trigger 역할), Polling(일정 주기 마다 Http or gRPC call)...


## 트랜잭션 패턴

- `2PC (2Phase Commit)`
  - 트랜잭션 완료를 2(N) 단계를 거쳐서 결정
  - Commit Request(1Phase) -> 정말 Commit 해되 되니?? -> 성공 시 Commit/ 실패시 Rollback(2Phase)
 
- Compensating Transactions(보상 트랜잭션)
  - 특정 요청과 그 요청에 대해 정상적이고 완전히 종료된 행동을 그 이전 상태로 되돌리기 위한 행동
 
- Saga Pattern(사가 패턴)
  - 트랜잭션의 선 후 관계를 사전에 정의하고 필요와 경우에 따라 Cordinator가 보상 트랜잭션을 이용, 관리하여 분산 시스템 환경에서 트랜잭션을 구현하기 위한 패턴
