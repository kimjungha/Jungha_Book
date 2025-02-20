## log 찍을때 request 값 주의 => LogInjection 야기

* Request 로 들어온 값을 그대로 로그에 작성하게 되면,  Log Injection 공격이 발생할 수 있다.
    * Log Injection : 공격자가 특수문자등을 이용해 로그파일을 변조하거나, 조작된 로그 삽입하여 공격

```java
public void solution(String description){
    log.debug("문제 설명 ==>" + description);
}
```

## 🔒 **해결 방법**

1. 입력값을 직접 로그에 기록하지 않는다.
   2. 로그에는 데이터 전체를 출력하지 않고, 상태만 로깅하는것이 안전
   3. `log.debug("문제 설명 존재 여부 :{}",(description !=null));`
   

2. 입력값을 escape(정화) 처리하여 안전하게 출력한다.
   3. escape : 특수문자를 안전한 문자로 변환하는 과정을 의미, 문자 그대로 출력해야할때 또는 공격을 방지하기 위해 필수적!
      4. ```java
         import org.apache.commons.text.StringEscapeUtils;
         public void solution(String description) {
           String sanitizedDescription = StringEscapeUtils.escapeJava(description);
           log.debug("문제 설명 ==>{}", sanitizedDescription);
         }
         ```
         공격자가 입력한 \n 이 그대로 출력되어, 로그가 변조되지 않으며 문자열로 기록되므로 공격 무효화

3. 민감한 데이터는 마스킹(masking) 처리한다.  
```java
public void solution(String description) {
    String sanitizedDescription = description.replaceAll("[\n\r]", "_"); // 개행문자 제거
    log.debug("문제 설명 ==>{}", sanitizedDescription);
}
```

## Escape 처리 또는 필터링을 적용해야하며, 최대한 저런 로그는 지양하기!