# Kotlin


* 타입 추론(Type Inference) 덕분에 타입선언 없이 사용가능
  * val place = "jungle" => 자동으로 String으로 추론됨
  * 그러나, null 을 바로 대입하게 되면 타입추론이 불가하기에 타입을 명시해야한다. 
  * ``val name = null // 오류 발생 cannot infer a type for a variable name``
  * ``val name: String? = null // 타입 명시하면 문제 없음 ``
  * 명시적으로 타입을 지정하면 가독성, 안정성을 높일수있고, 코드보는 사람이 쉽게 이해가 가능해서 쓰는편이 좋다!
  
  
* val 은 읽기 전용 변수로 , 자동으로 getter만 생성된다.
* var 은 변경(mutable) 가능 변수로, 자동으로 getter,setter 생성된다. 

* Null 안전성 (Null safety)
  * kotlin 은 null safety 를 제공하여 NullPointerException(NPE) 을 방지할 수 있는 언어
    * 변수를 선언할때 null 를 허용할지에 대해 구분해야한다. 
    * ? 를 붙이면 null 저장 가능 / 기본적으로 null 허용 안함
  * 🖍️ Safe Call (?.) 연산자를 사용하면 null 을 안정적으로 처리도 가능하다
    * Safe Call 연산자는 변수가 null 인지 먼저 체크후에, null 이 아닌 경우에만 행동하도록 동작
    * 밑에서 name이 null 인지 확인후에, null 이면 length 메서드를 호출하지 않아서 NPE 발생 안함
    * ````kotlin
      val name: String? = null
      println(name?.length)  // null (NPE 발생하지 않음)

  * 🖍️ Elvis 연산자 (?:) nullable 값이 null 일경우 기본값을 지정할수있다. 
  * ````kotlin
        val name: String?= null 
        val length = name?.length ?: 0