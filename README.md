# whois_spring_study

* 참고 도서 : 스프링 5와 Vue.js 2로 시작하는 모던 웹 애플리케이션 개발 (NAVER D2 지원)
> 08. 애플리케이션 뼈대 만들기, 09. 폼과 검증 - 회원가입 페이지부터 시작하기 단원 진행 중.  
책에 있는 홈페이지를 만들어 보면서 스프링을 익히는 과정으로 공부를 진행하고 있음.

### 스프링 이니셜라이저로 백엔드 뼈대 생성
[spring initializr](https://start.spring.io)

* Group : com.taskagile
* Artifact : app
* Name : TaskAgile
* Description : Open source task management tool
* Package Name : com.taskagile
* Dependencies : Web, Thymeleaf, JPA, DevTools
 ![](1.png)

### 파일 구조
![](2.png)

* `pom.xml` : 메이븐의 환경설정 파일
* `TaskAgileApplication.java` : 애플케이션의 시작점
* `TaskAgileApplicationTests.java` : 위 클래스의 단위 테스트

처음 `$mvn install` 명령어로 빌드를 시작하면 빌드 실패가 뜸.

``` xml
<dependency>
	<groupId>mysql</groupId>
	<artifactId>mysql-connector-java</artifactId>
</dependency>
```  
> `pom.xml` 파일에 추가

```
spring.datasource.url=jdbc:mysql://localhost:3306/task_agile?useSSL=false
spring.datasource.username=<mysql username>
spring.datasource.password=<mysql password>
```
> `application.properties`에 추가

데이터베이스 드라이버와 데이터 소스를 설정하지 않아서 빌드 실패 뜬 것. 두 가지 과정을 거치면 빌드에 성공함.	

### 프론트엔드 뼈대 생성
```
$ npm install -g @vue/cli
$ vue create front-end
```

```
$ cd front-end
$ npm run serve
```
![](3.png)

### 정리와 재구성
필요 없는 코드를 지우고 페이지를 공백으로 만들었음.

![](4.png)

``` javascript
import Vue from 'vue'
import LoginPage from '@/views/LoginPage'

describe('LoginPage.vue', () => {
	it('should render correct contents', () => {
		const Constructor = Vue.extend(LoginPage)
		const vm = new Constructor().$mount()
		expect(vm.$el.querySelector('h1').textContent)
		.toEqual('TaskAgile')
	})
})
```
> jest 테스트 파일 `LoginPage.spec.js`
