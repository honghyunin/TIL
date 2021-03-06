#  직렬화 (Serialization)


__직렬화 는 자료구조 혹은 객체 상태를 저장(파일, 메모리 버퍼, 네트워크로 전송 등) 되어 사용될 수 있는 포멧으로 변환하는 것을 말합니다.__ 그리고 다른 컴퓨터 환경에서 같은 것으로 재조립이 가능합니다.

바이트 스트림과 같은 전형적인 폼으로 부터 구조화된 데이터를 복사해 오는 것과 관련된 것입니다. 이런 의미에서 직렬화는 마샬링을 수행하기 위한 한 수단으로 볼 수 있고 보통 [Pass By Value](#Pass-By-Value)으로 수행됩니다.

<hr>

# 마샬링(Marshalling)

__객체의 메모리 표현을 저장공간 또는 전송에 적합한 데이터 포멧으로 변환하는 과정__ 입니다. 이것은 데이터가 프로그램에서 다른 프로그램으로 이동할 때 전형적으로 사용됩니다.

<hr>

직렬화의 과정에 마샬링이 포함되며, 실제로 객체 전송은  아래와 같은 순서로 진행된다. 고로 직렬화를 마샬링이라고 해도 무관합니다.

1. 직렬화된 객체를 바이트 단위로 분해합니다. (marshalling)
2. 직렬화 되어 분해된 데이터를 순서에 따라 전송합니다.
3. 전송 받은 데이터를 원래대로 복구합니다. (unmarshalling)

직렬화와의 가장 큰 차이점은 직렬화는 __객체__ 가 대상이지만 마샬링은 변환자체에 목적이 있기 때문에, 대상과 변환할 오브젝트가 한정되지 않습니다. 그렇기 때문에 서로 다른 언어간의 데이터 전송은 직렬화라고 하지 않고 마샬링이라고 합니다.

<hr>

# 정리

__직렬화__ 는 ``자료구조나 객체를 다른 형태로 변환시키는 것``


__마샬링__ 은 ``다른 언어 혹은 다른 플랫폼에서 서로 데이터를 주고 받을 때 쓰는 용어``

<hr>

### Pass By Value & Pass By Reference

<br>

#### Pass By Value

```c
int main(){
	int main_a = 5;
	foo(main_a);
	return;
}
void foo(int a){
	x += 1;
}
```

이러한 함수가 있을 때

main 함수에 있는 main_a는 foo가 호출됨으로써 main_a의 값이 증가하면

``pass by reference`` 아니면 ``pass by value``입니다.

 

``내부에 있는 필드의 값이 외부에 의해 변형되지 않고 값만 복제되어 사용하는 것``을 __pass by value__ 라고 합니다.

### pass by reference

- ``내부에 있는 필드의 값이 외부에 의해 변형이 될 때`` __``pass by reference``__  라고 부릅니다.

<hr>