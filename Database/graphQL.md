# GraphQL

graphQL은 API를 위한 쿼리 언어이며 타입 시스템을 사용하여 쿼리를 실행하는 서버사이드 런타임이다.

GraphQl은 특정한 DB나 스토리지 엔진과 관계되어 있지 않으며 기존 코드와 데이터에 의해 대체된다.

GraphQL 서비스는 타입과 필드를 정의하고, 각 타입의 필드에 대한 함수로 구현된다. 예를 들어, 로그인한 사용자가 누구인지(me)와 해당 사용자의 이름(name)을 가져오는 GraphQL 쿼리는 다음과 같다.

```graphQL
type Query {
	me: User
}

type User {
	id: ID
	name: String
}
```

각 타입 필드에 대한 함수를 작성하면 다음과 같다.

```
function Query_me(request) {
	return request.auth.user;
}

function User_name(user) {
	return user.getName();
}
```

아래는 쿼리 예제입니다.

```
{
	me {
		name
	}
}
```

다음과 같은 JSON을 얻게 됩니다.

```
{
	"me": {
		"name": "Luke Skywalker"
	}
}
```

