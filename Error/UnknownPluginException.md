# org.gradle.api.plugins.UnknownPluginException: Plugin was not found in any of the following sources:

오랜만에 프로젝트를 생성하고 세팅을 하던 도중 만난 에러입니다.

```java
Plugin [id: 'org.springframework.boot', version: '2.5.5'] was not found in any of the following sources:

- Gradle Core Plugins (plugin is not in 'org.gradle' namespace)

- Plugin Repositories (could not resolve plugin artifact 'org.springframework.boot:org.springframework.boot.gradle.plugin:2.5.5')

  Searched in the following repositories:

    Gradle Central Plugin Repository

* Try:

Run with --info or --debug option to get more log output. Run with --scan to get full insights.

* Exception is:

org.gradle.api.plugins.UnknownPluginException: Plugin [id: 'org.springframework.boot', version: '2.5.5'] was not found in any of the following sources:

- Gradle Core Plugins (plugin is not in 'org.gradle' namespace)

- Plugin Repositories (could not resolve plugin artifact 'org.springframework.boot:org.springframework.boot.gradle.plugin:2.5.5')
```

위 오류는 build.gradle이 해당 plugin을 설치할 수 없거나 이상이 있을 때 발생하는 에러입니다.

# 해결방법

1. Intellij JDK, SDK 확인
	1. File -> Project
	   ![[Pasted image 20220825141536.png]]
	2. Inetllij Settings -> Build -> Gradle
	   ![[Pasted image 20220825135801.png]]
	   Build and run using : `Intellij IDEA`
	   Run tests using : `Intellij IDEA`
	   
	   Gradle JVM : 자바 버젼에 맞게 설정
2. 인터넷 인증서 보안 때문에 첫 build.gradle 빌드가 되지 않을 수 있습니다.
	1. 인증서 등록을 통해 해당 인터넷에서 빌드할 수 있도록 설정합니다.