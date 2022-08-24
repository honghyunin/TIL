# 동시성 & 비동기 / 프로그래밍

## 프로세서란?

- 프로세서는 컴퓨터 하드웨어 측면에서 프로그램을 수행하는 하드웨어 유닛이라 합니다. 대표적으로 중앙처리장치를 마라며 컴퓨터 한대가 여러 프로세서를 갖는다면 멀티 프로세서라 합니다.

## 코어

- 프로세서의 코어는 주요 연산회로인데. 싱글코어는 연산회로가 하나인 것을 말하고 듀얼 코어는 연산회로가 두 개가 내장되어 있음을 말합니다. 멀티코어는 여러개의 연산회로를 말합니다.

## 프로그램과 프로세스

- 프로그램은 일반적으로 보조기억장치에 저장된 실행코드 즉 생명이 없는 상태를 말합니다. 동시에 여러개의 프로세스를 운용하는 것을 멀티태스킹이라 하며 이는 운영체제에서 담당합니다.
## 스레드

- 스레드는 프로세스 내에서 실행되는 작업흐름의 단위를 말합니다. 보통 한 프로세스는 하나의 스레드를 갖고 있는데 프로세스의 환경에 따라 동시에 둘 이상의 스레드를 실행할 수 있습니다. 이러한 방식을 멀티스레딩이라고 합니다. 그리고 프로그램이 시작될 때 동작하는 스레드를 메인스레드 나중에 생성된 스레드를 서브 스레드 또는 세컨더리 스레드입니다.

# 비동기(Asynchronous) 프로그래밍

- 프로그램의 주 실행 흐름을 멈추어서 기다리는 부분 없이 바로 다음 작업을 실행할 수 있게 하는 방식입니다. 즉 코드의 실행 결과를 별도의 공간에 맡겨둔 뒤 결과를 기다리지 않고 다음 코드를 실행하는 병렬처리 방식입니다.

# 동시성(Concurrency) 프로그래밍

- 논리적인 용어로 동시에 실행되는 것을 말합니다. 싱클코어에서 멀티스레드를 동작시키기 위한 방식으로 멀티 태스킹을 위해 여러 스레드를 번갈아 가면서 실행되는 방식입니다.


# 병렬성 프로그래밍

- 물리적으로 정확히 동시에 실행되는 것을 말합니다. 멀티 코어에서 멀티 스레드를 실행시키는 방식으로 데이터 병렬성과 작업 병렬성으로 나뉩니다.


# 데이터 병렬성

- 전체 데이터를 나누어 서브 데이터들로 만든 뒤, 서브 데이터들을 병렬 처리해서 작업을 빠르게 수행하는 방법입니다.

# 작업 병렬성

- 서로 다른 작업을 정렬 처리하는 것을 말합니다.


# 동시성과 병렬성의 차이

- 동시성 프로그래밍과 병렬성 프로그래밍 모두 비동기로 동작을 구현할 수 있지만, 그 동작 원리가 다릅니다.

![Concurrency & Parallelism](/images/Concurrency&Parallelism.png)

## 동시성

- 통장을 만들어온 n개의 대기열과 한 명 이상의 은행직원

## 병렬성

- 통장을 만들러온 n개의 대기열과 n명의 은행직원
