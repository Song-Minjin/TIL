# Spring JPA를 활용한 CRUD

## Create
**👉🏻 `Repository`의`save()` 이용**
```java
repository.save(new Post("철수의 TIL", "김철수", "오늘 배운 것 : REST API"))
```

<br>

## Read
**👉🏻 `Repository`의 `findAll()` 이용**
```java
// 데이터 전부 조회하기
List<Post> postList = repository.findAll();
for (int i=0; i<postList.size(); i++) {
    Post post = postList.get(i);
    System.out.println(post.getId());
    System.out.println(post.getTitle());
	System.out.println(post.getAuthor());
   	System.out.println(post.getContent());
}

// 데이터 하나 조회하기
Post post = repository.findById(1L).orElseThrow(
        () -> new IllegalArgumentException("해당 게시글이 존재하지 않습니다.")
);
```

<br>

## Update
**👉🏻 `Repository`의 `findAll()`과 `Service`의 `update()` 이용**

```java
@Bean
public CommandLineRunner demo(PostRepository postRepository, PostService postService) {
    return (args) -> {
        postRepository.save(new Post("프론트엔드의 꽃, 리액트", "임민영"));

        System.out.println("데이터 인쇄");
        List<Post> postList = postRepository.findAll();
        for (int i=0; i<postList.size(); i++) {
            Post post = postList.get(i);
            System.out.println(post.getId());
            System.out.println(post.getTitle());
            System.out.println(post.getAuthor());
        }

        Post new_post = new Post("웹개발의 봄, Spring", "임민영");
        postService.update(1L, new_post);
        postList = postRepository.findAll();
        for (int i=0; i<posstList.size(); i++) {
            Post post = postList.get(i);
            System.out.println(post.getId());
            System.out.println(post.getTitle());
            System.out.println(post.getAuthor());
        }
    };
}
```

> 💡 **Tip!**<br>
> 
> 사실 지금 Update 기능만 Service를 이용한 것 같아 보이지만, repository의 메소드들을 사용하지만 서버에서 처리하는 복잡한 작업들은 웬만하면 Service에 넣어주는 것이 깔끔하다.<br>
> 즉, 위에서 정리한 것처럼<br>
> **Controller**에는 프론트와 소통해야 하는 필수 부분들만,<br>
> **Service**에는 그 외,<br>
> **Repository**에는 DB와 소통해야 하는 필수 부분들만 넣어주는 것<br>
> 이 깔끔하고 보기 좋은 코드라고 한다.

<br>

## Delete
**👉🏻 `Repository`의 `findAll()`과 `deleteAll()` 이용**

```java
@Bean
public CommandLineRunner demo(PostRepository postRepository, PostService postService) {
    return (args) -> {
        postRepository.save(new Post("프론트엔드의 꽃, 리액트", "임민영"));

        System.out.println("데이터 인쇄");
        List<Post> postList = postRepository.findAll();
        for (int i=0; i<postList.size(); i++) {
            Post post = postList.get(i);
            System.out.println(post.getId());
            System.out.println(post.getTitle());
            System.out.println(post.getTutor());
        }

        Post new_post = new Post("웹개발의 봄, Spring", "임민영");
        postService.update(1L, new_post);
        postList = postRepository.findAll();
        for (int i=0; i<postList.size(); i++) {
            Post post = postList.get(i);
            System.out.println(post.getId());
            System.out.println(post.getTitle());
            System.out.println(post.getTutor());
        }

        postRepository.deleteAll();
    };
}
```