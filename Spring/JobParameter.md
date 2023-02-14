# JobParameter와 Scope

JobParameter는 `@RequestParam` 처럼 command line 실행 시에 따로 값을 주어 변수로 활용할 수 있는 어노테이션이다.

`@JobScope`는 Step 선언문에서 사용 가능하고, `@StepScope`는 Tasklet이나 ItemReader, ItemWriter, ItemProcessor에서 사용할 수 있다.

현재 Job Parameter의 타입으로 사용할 수 있는 것은 Double, Long, Date, String이 있다
아쉽지만 LocalDate와 LocalDateTime이 없어 String으로 받아 타입변환을 해서 사용해야만 한다.

Job Parameter의 할당은 어플리케이션 실행 시에 하지 않는다.

## @StepScope & @JobScope 소개

Spring Batch는 두 개의 Bean Scope를 지원한다

Spring Bean의 기본 Scope는 singleton이다.

그러나 Spring Batch 컴포넌트(Tasklet, ItemReader, ItemWriter, Processor 등)에 @StepScope를 사용하게 되면 Spring Batch가 Spring 컨테이너를 통해 지정된 Step의 실행 시점에 해당 컴포넌트를 Spring Bean으로 생성한다.
즉, Bean의 생성 시점을 지정된 Scope가 실행되는 시점으로 지연시킨다.

Bean 생성 시점을 Step, Job의 실행 시점으로 지연시킬 경우 얻는 이점

1. 비지니스 로직 처리 단계(Controller, Service, StepContext, JobExecutioContext) 레벨에서 할당할 수 있다
2. 동일한 컴포넌트를 병렬, 동시에 사용할 때 각각의 Step에서 별도의 Tasklet을 생성하고 관리하여 서로의 상태를 침범하지 않는다

## JobParameter 오해

Job Parameter는 `@Value`를 통해 가능하다
그러다보니 시스템 변수로 CommandLineRunner 실행 시에 변수를 주어 실행하면 되는 것이라고 생각할 수 있지만
그렇게 값을 주게 될 경우 Job Parameter 관련 기능을 못쓰게 된다.

예를 들어 Spring Batch는 Job Parameter로 같은 Job을 두 번 실행하지 않는다

하지만 시스템 변수를 사용할 경우 이 기능이 전혀 작동하지 않는다
또한 자동으로 관리해주는 Parameter 관련 메타 테이블이 전혀 관리되지 않는다.

또한 Command Line이 아닌 다른 방법으로 Job을 실행하기가 매우 어렵다
만약 실행한다면 전역 상태(시스템 변수 혹은 환경 변수)를 동적으로 계속해서 변경시킬 수 있도록 Spring Batch를 구성해야 한다
동시에 여러 Job을 실행하려는 경우 또는 테스트 코드로 Job을 실행해야할 때 문제가 발생할 수 있다.
