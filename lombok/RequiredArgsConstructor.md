## @RequiredArgsConstructor (Lombok 활용)

@RequiredArgsConstructor 롬복 사용하면 생성자 직접 작성할 필요없이
자동으로 private final 필드에 대한 생성자를 생성해준다.

코드를 더 간결하게 유지 가능하다. 

```java
    @Service
    @RequiredArgsConstructor
    public class BookService{
        private final BookRepository bookRepository;
        // service method
        }

