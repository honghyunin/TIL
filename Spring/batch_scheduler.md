
# Spring Batch, Scheduler 차이

**배치(Batch)** 란?

> **배치(Batch) : 일괄처리**
> 사용자와 상호작용 없이 대용량 작업을 미리 정해진 순서에 따라 중단 없이 처리하는 작업을 의미합니다.

**스케줄러(Scheduler)란?**

> 특정한 시간에 등록한 작업을 자동으로 실행시키는 것
> -> Spring Scheduler, Quartz 등

**Spring Batch**

Spring Batch는 로깅/추적, 트랜잭션 관리, 작업 처리 통계, 작업 재시작, 건너뛰기 등 대용량 레코드 처리에 필수적인 기능을 제공합니다. 또한 최적화 및 파티셔닝 기술을 통해 대용량 및 고성능 배치 작업을 가능하게 하는 고급 기술 서비스 및 기능을 제공합니다.

Spring Batch에서 배치가 실패하여 작업 재시작을 할 경우 처음부터가 아닌 실패한 지점에서 실행하게 됩니다.
또한 중복 실행을 방지하기 위해 성공한 이력이 있는 Batch는 동일한 Parameters로 실행 시 Exception이 발생하게 합니다.

**Spring Batch VS Quartz? Scheduler?**

Spring Batch는 Job을 관리하지만, Job을 구동, 실행 기능은 지원하지 않습니다. Spring에서 Batch Job을 실행하기 위해서는 Quartz, Scheduler, Jenkins등 전용 Scheduler를 사용해야 합니다.
