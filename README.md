# com.lotte.drssa

**Spring Boot로 만든 웹 애플리케이션의 시작용(뼈대) 프로젝트**입니다.
2018년 2월에 만들어졌고, 아직 화면이나 API를 처리하는 코드(컨트롤러, JSP 등)는 들어 있지 않습니다.
앞으로 기능을 붙여 나가기 위한 빈 틀이라고 보면 됩니다.

## 지금 들어 있는 것

| 구분 | 내용 |
| --- | --- |
| 실행 시작점 | `Application.java` (`main` 메서드로 서버 실행) |
| 외부 Tomcat 배포용 | `ServletInitializer.java` (WAR 파일을 Tomcat에 올릴 때 사용) |
| 화면(JSP) 설정 | `/WEB-INF/jsp/` 폴더의 `.jsp` 파일을 화면으로 사용하도록 설정됨 |
| 테스트 | `ApplicationTests.java` (스프링이 정상 시작되는지만 확인) |

## 사용 기술

| 구분 | 내용 |
| --- | --- |
| 언어 | Java (`pom.xml`의 `java.version` = 1.7) |
| 프레임워크 | Spring Boot 1.5.10.RELEASE |
| 빌드 도구 | Maven (Maven Wrapper 포함, Maven 3.5.2) |
| 배포 형태 | WAR |
| 포함된 기능 모음(starter) | web, web-services, websocket, tomcat(`provided`), test, JSTL |

## 폴더 구조

```
com.lotte.drssa/
├── pom.xml                                   # 라이브러리·빌드 설정
├── mvnw, mvnw.cmd                            # Maven Wrapper (Maven을 따로 설치하지 않아도 됨)
├── .mvn/wrapper/                             # Maven Wrapper 설정
└── src/
    ├── main/
    │   ├── java/com/lotte/drssa/
    │   │   ├── Application.java              # 실행 시작점
    │   │   └── ServletInitializer.java       # 외부 Tomcat 배포용
    │   └── resources/
    │       └── application.properties        # 설정 파일
    └── test/java/com/lotte/drssa/
        └── ApplicationTests.java             # 시작 확인 테스트
```

## 설정 (`application.properties`)

| 이름 | 값 | 설명 |
| --- | --- | --- |
| `spring.mvc.view.prefix` | `/WEB-INF/jsp/` | 화면 파일이 있는 폴더 |
| `spring.mvc.view.suffix` | `.jsp` | 화면 파일 확장자 |

그 밖의 설정(예: 포트)은 지정하지 않아서 스프링 부트 기본값을 따릅니다.

## 실행 방법

### 1. 준비물

- JDK 8 (프로젝트가 Java 1.7 기준의 오래된 설정이라 JDK 8을 권장합니다. 최신 JDK는 `pom.xml`의 `java.version` 조정이 필요할 수 있습니다.)
- 인터넷 연결 (처음 실행할 때 라이브러리를 내려받습니다.)

### 2. 내려받기

```bash
git clone https://github.com/jeong-jihyun/com.lotte.drssa.git
cd com.lotte.drssa
```

### 3. 서버 실행

```bash
# Mac / Linux
./mvnw spring-boot:run

# Windows
mvnw.cmd spring-boot:run
```

서버가 시작되면 http://localhost:8080 으로 접속합니다 (포트는 스프링 부트 기본값 8080).
아직 화면을 만드는 코드가 없으므로, 접속해도 보여 줄 페이지는 없습니다.

### 4. WAR 파일 만들기

```bash
./mvnw clean package
```

`target/` 폴더에 `com.lotte.drssa-0.0.1-SNAPSHOT.war`가 만들어집니다. 외부 Tomcat에 올리거나 `java -jar`로 실행할 수 있습니다.

## 화면(JSP) 추가하는 방법

설정이 `/WEB-INF/jsp/`를 가리키므로, 아래 위치에 JSP 파일을 만들고 컨트롤러에서 파일 이름으로 연결하면 됩니다.

```
src/main/webapp/WEB-INF/jsp/파일이름.jsp
```

## 앞으로 손보면 좋은 점

- 컨트롤러, 화면(JSP), 서비스 코드를 추가해야 실제로 동작하는 앱이 됩니다.
- `pom.xml`의 프로젝트 설명이 기본 문구("Demo project for Spring Boot")입니다. 실제 용도에 맞게 바꾸면 좋습니다.
- `web-services`, `websocket` 기능 모음이 포함되어 있지만 이를 쓰는 코드는 아직 없습니다. 쓰지 않는다면 `pom.xml`에서 빼도 됩니다.
- Spring Boot 1.5.x와 Java 1.7 설정은 오래된 버전이라 새로 개발을 이어간다면 버전 올리기를 검토하세요.
- 테스트는 "스프링이 시작되는지" 확인하는 1개뿐입니다.
