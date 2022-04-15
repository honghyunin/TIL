# Java Code Conventions

# CamelCase

카멜케이스란 단어가 합쳐진 부분마다 맨 첫 글자를 대문자로 표기하는 방법입니다.

ex) MegaBox, MovieStar

CamelCase는 lowerCamelCase와 UpperCamelCase로 세부적으로 나눌 수 있습니다

## lowerCamelCase

camelCase에서, 맨 앞글자를 소문자로 표기하는 것을 뜻합니다.

나머지 뒤에 따라붙는 단어들의 앞글자는 모두 대문자로 표기합니다.

## UpperCamelCase (=PascalCase)

CamelCase에서, 맨 앞글자를 대문자로 표기하는 것을 뜻합니다. **PascalCase**라고도 불립니다.

나머지 뒤에 따라붙는 단어들의 앞글자는 모두 대문자로 표기합니다.

ex) CamelCase, NamingConvention...

## snake_case

scane_case는 단어가 합쳐지는 부분마다 언더라인(_) 또는 하이픈(-)을 사용합니다.

snake_case에는 Train_case와 spinal_case로 나누어 집니다.

## Train_Case

Snake_Case에서, 각 단어의 맨 앞글자를 대문자로 표기하는 것을 의미합니다.

## spinal_case

snake_case에서, 각 단어의 맨 앞글자를 소문자로 표기하는 것을 의미합니다.

## Class

- 클래스 이름은 명사이고, 복합 단어일 경우 각 단어의 첫 글자는 대문자이어야 합니다.

## Interface

- 인터페이스 또한 클래스와 같이 대문자 사용 UpperCamelCase를 사용한다.

## Methods

- 메서드의 이름은 동사이어야 하며, 복합 단어일 경우 첫 단어는 소문자로 시작하고 그 이후에 나오는 단어의 첫 문자는 대 문자로 사용해야한다.

## Variables

- 변수 이름의 첫 번째 문자는 소문자로 시작하고, 각각의 내부 단어의 첫 번째 문자는 대문자로 시작해야 한다.
- 이름은 그 변수의 사용 의도를 알아낼 수 있도록 해야한다.

## Constans

- 클래스 상수로 선언된 변수들과 ANSI 상수들의 이름은 모두 대문자로 쓰고 각각의 단어는 언더바("_")로 분리 해야 한다.

예시)
static final int MIN_WIDTH = 4;