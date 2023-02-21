# What is Quartz?

다양한 Java 애플리케이션에 통합할 수 있는 작업 스케줄링 라이브러리입니다

# Qurtaz의 구성 요소

## Job, JobDetail

**Job**은 **Quartz Scheduler**로 **실행할 작업**을 의미합니다. 
Quartz의 Job 인터페이스의 `execute` 메서드를 구현하고, 
메서드 안에는 **Scheduler가 실제로 수행할 작업을 작성**합니다.

**JobDetail**은 위에서 작성한 `execute` 메서드를 실제로 언제 실행시킬지에 대한 작업을 정의합니다.

**JobBuilder**는 위 **JobDetail 인터페이스의 구현체를 생성하기 위한 빌더 클래스**이며 
인스턴스 정의에 필요한 정보를 필요한 만큼 부여해 생성할 수 있습니다.

## JobDataMap

Qurtaz Scheduler는 작업을 생성하여 실행하고 종료 시 참조를 삭제하여 가비지 컬렉터가 제거하는 생명 주기를 반복합니다.

따라서 클래스 필드로서는 작업끼리의 상태를 유지할 수 없지만, JobDataMap을 통해 작업 실행 간 상태를 공유할 수 있습니다.

JobDataMap은 JobBuilder를 통해 등록하고 스케줄러에 작업이 등록될 때 같이 등록됩니다. 이름에서 추측할 수 있듯이 Job과 관련된 데이터를 저장하는 Map 자료구조로, 특정 Job 인스턴스의 상태 정보를 담고 있습니다.

이런 JobDataMap은 설정에 따라 Memory 혹은 DB에 저장될 수 있습니다. 후자의 경우 직렬, 역직렬화를 수행하기 때문에 별도의 주의가 필요할 수 있습니다.

## Trigger

Trigger는 Job이 실행할 시간, 방법을 정의합니다.

Qurtaz에서는 가장 기본적인 두 가지 방식의 스케줄링을 제공하는데 일정 간격으로 n번 반복하는 simple 방식과 Cron 표현식을 이용한 cron 방식을 제공합니다.

[Cron 표현식 정리](https://github.com/honghyunin/TIL/blob/main/Spring/Cron.md)

## JobListener

Job이 실행될 때의 이벤트 정보를 담고 있습니다. Job이 실행 되기 전, 중단, 실행 완료 후 각종 이벤트를 넣어줄 수 있습니다.

## TriggerListener

Trigger가 실행될 때의 이벤트 정보를 담고 있습니다.

## Scheduler

Scheduler는 스케줄을 관리하는 객체입니다.

JobDetail과 Trigger 인스턴스를 관리하고 Trigger가 실행될 때 JobDetail을 기반으로 작업을 실행시킵니다. 스케줄러 인스턴스는 SchedulerFactory를 통해 생성할 수 있고, Spring Boot 사용 시 설정 파일에 따라 컨테이너 스케줄러 인스턴스를 등록하며 이를 주입 받아 스케줄러에 작업을 등록하거나 트리거를 설정할 수 있습니다.

# Quartz Scheduler 설정

| Property Name | Req'd | Type | Default Value |
| --- | --- | --- | --- |
| org.quartz.scheduler.instanceName | no | string | 'QuartzScheduler' |
| org.quartz.scheduler.instanceId | no | string | 'NON_CLUSTERED' |
| org.quartz.scheduler.instanceIdGenerator.class | no | string (class name) | org.quartz.simpl.SimpleInstanceIdGenerator |
| org.quartz.scheduler.threadName | no | string | instanceName+ '_QuartzSchedulerThread' |
| org.quartz.scheduler.makeSchedulerThreadDaemon | no | boolean | false |
| org.quartz.scheduler.threadsInheritContextClassLoaderOfInitializer | no | boolean | false |
| org.quartz.scheduler.idleWaitTime | no | long | 30000 |
| org.quartz.scheduler.dbFailureRetryInterval | no | long | 15000 |
| org.quartz.scheduler.classLoadHelper.class | no | string (class name) | org.quartz.simpl.CascadingClassLoadHelper |
| org.quartz.scheduler.jobFactory.class | no | string (class name) | org.quartz.simpl.PropertySettingJobFactory |
| org.quartz.context.key.SOME_KEY | no | string | none |
| org.quartz.scheduler.userTransactionURL | no | string (url) | 'java:comp/UserTransaction' |
| org.quartz.scheduler.wrapJobExecutionInUserTransaction | no | boolean | false |
| org.quartz.scheduler.skipUpdateCheck | no | boolean | false |
| org.quartz.scheduler.batchTriggerAcquisitionMaxCount | no | int | 1 |
| org.quartz.scheduler.batchTriggerAcquisitionFireAheadTimeWindow | no | long | 0 |

## **org.quartz.scheduler.instanceName**

스케줄러 인스턴스의 이름을 의미합니다.

동일한 프로그램 내에서 여러 인스턴스가 사용되는 경우 스케줄러를 구분하는 프로퍼티입니다.

클러스터링을 사용하는 경우 모든 인스턴스에서 동일한 스케줄러를 ‘논리적’으로 사용할 필요가 있습니다

## **org.quartz.scheduler.instanceId**

모든 스케줄러가 동일한 ‘논리적인’ 스케줄러인 것처럼 작업하는 경우 고유해야 합니다. 

클러스터 ID를 생성하는 경우 값 “AUTO”를 instanceID로 사용할 수 있습니다. 

- `org.quartz`에서 값을 가져오려면 “SYS_PROP”을 선택하여 가져올 수 있습니다.

## **org.quartz.scheduler.instanceIdGenerator.class**

org.quartz.scheduler.instanceId 설정이 “AUTO”일 경우에만 사용됩니다.

호스트 이름 및 타임스탬프를 기준으로 인스턴스 ID를 생성합니다

InstanceIdGenerator 인터페이스를 구현하여 직접 호스트 이름 생성 로직을 커스텀 해 작성할 수 있습니다

## **org.quartz.scheduler.threadName**

스케줄러가 실행되면서 사용할 스레드의 이름을 지정할 수 있습니다

설정하지 않을 경우 `org.quartz.scheduler.instanceName` 의 이름으로 스레드 이름이 지정됩니다

## **org.quartz.scheduler.makeSchedulerThreadDaemon**

Boolean 값에 따라 스케줄러의 주 스레드가 데몬 스레드 여부를 결정합니다

## **org.quartz.scheduler.idleWaitTime**

스케줄러가 멈춰있을 때 사용 가능한 트리거를 재실행하기 전에 대기하는 시간입니다.

XA 트랜잭션을 사용하고 즉시 실행 될 트리거가 문제가 있는 경우가 아니라면 이 옵션을 조정할 필요가 없습니다. 5000ms 미만의 값은 과도한 데이터베이스 쿼리를 유발하므로 권장되지 않습니다. 1000보다 작은 값은 부적합합니다.

## **org.quartz.scheduler.dbFailureRetryInterval**

스케줄러가 DB 연결에 실패한 경우 다시 연결하기까지 대기하는 시간입니다.

RamJobStore를 사용할 때 이 매개 변수는 딱히 의미가 없습니다.

## **org.quartz.scheduler.jobFactory.class**

사용할 JobFactory의 클래스 이름입니다.