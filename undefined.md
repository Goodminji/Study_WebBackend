# 빌더패턴

빌더 패턴의 장점

=&gt; 필수 인자값을 전달하여 빌더 객체를 만든  빌더 객체에 정의된 메서드를 호출해서 객체를 생성. 

* 필요한 데이터만 설정할 수 있음
* 유연성을 확보할 수 있음
* 가독성을 높일 수 있음
* 불변성을 확보할 수 있음

```text
 //User 클래
 public class User {

  private final Long seq;

  private final String name;

  private final Email email;

  public User(String name, Email email) {
    this(null, name, email);
  }

  public User(Long seq, String name, Email email) {
    
    this.seq = seq;
    this.name = name;
    this.email = email;
  }

  public Long getSeq() {
    return seq;
  }

  public String getName() {
    return name;
  }

  public Email getEmail() {
    return email;
  }
 

  @Override
  public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    User user = (User) o;
    return Objects.equals(seq, user.seq);
  }

  @Override
  public int hashCode() {
    return Objects.hash(seq);
  }

  @Override
  public String toString() {
    return new ToStringBuilder(this, ToStringStyle.SHORT_PREFIX_STYLE)
      .append("seq", seq)
      .append("name", name)
      .append("email", email)
      .toString();
  }

static public class Builder {
    private Long seq;
    private String name;
    private Email email;

    public Builder() {
    }

    public Builder(User user) {
      this.seq = user.seq;
      this.name = user.name;
      this.email = user.email;
    }

    public Builder seq(Long seq) {
      this.seq = seq;
      return this;
    }

    public Builder name(String name) {
      this.name = name;
      return this;
    }

    public Builder email(Email email) {
      this.email = email;
      return this;
    }


    public User build() {
      return new User(seq, name, email);
    }
  }
  
  // 생성할때 사용 방
 new User.Builder()
    .seq(rs.getLong("seq"))
    .name(rs.getString("name"))
    .email(new Email(rs.getString("email")))
    .build();
```

  
  
출처: [https://mangkyu.tistory.com/163](https://mangkyu.tistory.com/163) \[MangKyu's Diary\]

