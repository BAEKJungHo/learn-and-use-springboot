# API 개발

MSA(Micro Service Architecture) 개발이나 SPA(Single Page Application) 개발에서 API 연계는 필수다. 소매 업계에서는 `옴니 채널`(사용자가 채널의 차이를 의식하지 않고 서비스를 이용하거나
제품을 구입할 수 있는 것)이라는 단어가 생겨났다. 채널의 차이를 의식하지 않으려면 백엔드 서비스를 API 화하고 PC/스마트폰/기타 서비스 등 여러 채널에서 투명하게 사용할 수 있어야 한다.

스프링 부트에서 API 는 `@RestController` 로 구현한다.

## 사용자 정보 취득 요청에 JSON 을 반환하는 API

- 사용자 목록 취득 API
  - email
  - firstName
  - lastName
  - tel
  - zip
  - address
- 사용자 생성 API

## 리소스 구현

- 사용자 목록 취득용 클래스

네트워크를 통해서 전송하기 때문에 배열이나 컬렉션인 경우엔 Serializable 을 구현할 필요가 없지만 API 통신에서 직접 만든 클래스의 경우 Serializable 구현이 필수다.

```java
public class UserQuery implements Serializable {

  private static final long serialVersionUID = 759356324192730932L;
  
  String email;
  String firstName;
  String lastName;
  String tel;
  String zip;
  String address;

}
```

- 사용자 생성용 리소스 클래스

```java
@Getter @Stter
public class UserResource implements Serializable {

  private static final long serialVersionUID = 451263300585227922L;
  
  @JsonIgnore
  String password;
  
  @JsonProperty("firstName")
  String firstName;
  
  @JsonProperty("lastName")
  String lastName;
  
  @Email
  String email;
  
  @Digits(fraction = 0, integer = 10)
  String tel;
  
  @NotEmpty
  String zip;
  
  @NotEmpty
  String address;

}
```

