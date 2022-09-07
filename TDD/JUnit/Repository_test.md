# Repository 테스트

Repository는 Entity를 영속화하기 위해 사용하는 것이다. 이 Entity의 영속화는 Service 단에서 요구한다.
Service단에서 비즈니스 로직을 수행하고 난 Domain을 영속화해야 하는데, 이 기능을 Repository(저장소 영역)로 위임한다는 것이다.

➡ 따라서 Repository의 기능만 테스트하기 위해서는 Service와의 결합을 끊어야 한다!

<br>

SpringBoot의 테스트는 `@DataJpaTest` Annotation을 제공하는데, 이를 통해 Repository의 단위 테스트가 가능해진다.

**`@DataJpaTest`의 기능**

- JPA 관련된 설정만 로드한다. (WebMVC와 관련된 Bean이나 기능은 로드되지 않는다.)

- JPA를 사용해서 생성/조회/수정/삭제 기능의 테스트가 가능하다.

- `@Transactional`을 기본적으로 내장하고 있으므로, 매 테스트코드가 종료되면 자동으로 DB가 롤백된다.

- 기본적으로 내장 DB를 사용한다. (설정을 통해 실제 DB로 테스트도 가능하지만, 권장되지 않는다.)

- `@Entity`가 선언된 클래스를 스캔하여 저장소를 구성한다.

<br>

## Test 해보기

```java
@DataJpaTest
@AutoConfigureTestDatabase(replace = AutoConfigureTestDatabase.Replace.NONE)
class AnswerRepositoryTest {

    @Autowired
    AnswerRepository answerRepository;

    Member mockMember = Member.builder()
            .username("cheolsu")
            .password("password")
            .nickname("김철수")
            .build();

    Interview mockInterview = Interview.builder()
            .question("스프링이란?")
            .answer("웹 어플리케이션을 만들 수 있는 자바 기반의 웹 프레임워크이다.")
            .subTopic(SubTopic.builder()
                    .topic(Topic.builder()
                            .name("BACKEND")
                            .build())
                    .name("SPRING")
                    .build())
            .build();

    @BeforeEach
    void setUp() {

        MockMemberRepository memberRepository = new MockMemberRepository();
        memberRepository.save(mockMember);

        MockInterviewRepository interviewRepository = new MockInterviewRepository();
        interviewRepository.save(mockInterview);
    }

    @Test
    @DisplayName("save answer")
    void saveAnswer() {

        // given
        Answer answer = Answer.builder()
                .interview(mockInterview)
                .member(mockMember)
                .content("스프링은 자바 기반 프레임워크입니다.")
                .publicTF(true)
                .build();

        // when
        Answer savedAnswer = answerRepository.save(answer);

        // then
        Assertions.assertThat(answer).isSameAs(savedAnswer);
        Assertions.assertThat(answer.getContent()).isEqualTo(savedAnswer.getContent());
        Assertions.assertThat(answer.isPublicTF()).isEqualTo(savedAnswer.isPublicTF());
    }

    @Test
    @DisplayName("find answer")
    void findAnswer() {

        // given
        Answer answer1 = Answer.builder()
                .interview(mockInterview)
                .member(mockMember)
                .content("공개 답변 내용 1")
                .publicTF(true)
                .build();

        Answer answer2 = Answer.builder()
                .interview(mockInterview)
                .member(mockMember)
                .content("비공개 답변 내용 2")
                .publicTF(false)
                .build();

        Answer savedAnswer1 = answerRepository.save(answer1);
        Answer savedAnswer2 = answerRepository.save(answer2);

        // when
        Answer findAnswer1 = answerRepository.findById(savedAnswer1.getId())
                .orElseThrow(() -> new IllegalArgumentException("Wrong AnswerId:<" + savedAnswer1.getId() + ">"));
        Answer findAnswer2 = answerRepository.findById(savedAnswer2.getId())
                .orElseThrow(() -> new IllegalArgumentException("Wrong AnswerId:<" + savedAnswer2.getId() + ">"));

        // then
        Assertions.assertThat(findAnswer1.getInterview()).isEqualTo(mockInterview);
        Assertions.assertThat(findAnswer1.getMember()).isEqualTo(mockMember);
        Assertions.assertThat(findAnswer1.getContent()).isEqualTo("공개 답변 내용 1");
        Assertions.assertThat(findAnswer1.isPublicTF()).isEqualTo(true);
        Assertions.assertThat(findAnswer2.getContent()).isEqualTo("비공개 답변 내용 2");
        Assertions.assertThat(findAnswer2.isPublicTF()).isEqualTo(false);


    }
}
```