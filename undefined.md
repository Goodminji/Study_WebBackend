# 빌더패턴

빌더 패턴의 장

* 필요한 데이터만 설정할 수 있음
* 유연성을 확보할 수 있음
* 가독성을 높일 수 있음
* 불변성을 확보할 수 있음

```text
 new User.Builder()
    .seq(rs.getLong("seq"))
    .name(rs.getString("name"))
    .email(new Email(rs.getString("email")))
    .password(rs.getString("passwd"))
    .profileImageUrl(rs.getString("profile_image_url"))
    .loginCount(rs.getInt("login_count"))
    .lastLoginAt(dateTimeOf(rs.getTimestamp("last_login_at")))
    .createAt(dateTimeOf(rs.getTimestamp("create_at")))
    .build();
```

  
  
출처: [https://mangkyu.tistory.com/163](https://mangkyu.tistory.com/163) \[MangKyu's Diary\]

