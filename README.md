# swift-style-guide

Apple Developer Academy의 개발자들이 따르고 있는 스위프트 스타일 가이드입니다. 다른 사람의 코드를 읽을 때 가독성을 높여주며,
내가 코드를 작성할 때 애매한 부분을 제거해줘 생산성 향상에 도움을 줍니다!

취향에 문제가 많기 때문에 코드를 작성하는데 어려움이 생긴다면 PR을 통해 언제나 의견을 주세요.

기여를 하고싶으신 분들을 위한 가이드는 [컨트리뷰션 가이드라인](./.github/CONTRIBUTING.md)을 참고해주세요.




## 목차
  - [네이밍](#네이밍)
    - [변수](#변수)


## 네이밍
### 변수
- 변수 이름은 `lowerCamelCase`를 사용해주세요.
- 배열과 같이 복수의 의미를 담고있는 변수라면 끝에 **s**를 붙여서 사용해주세요.
  - **Good ✅**
    ```swift
    var categories: [String]
    var person: Person
    var isShowing: Bool
    ```
  - **Bad ❌**
    ```swift
    var category: [String]
    var show: Bool
    ```


## Reference
- [Google Swift Style Guide](https://google.github.io/swift/)
- [Airbnb Swift Style Guide](https://github.com/airbnb/swift)
- [Linkedin Swift Style Guide](https://github.com/linkedin/swift-style-guide)
- [Raywenderlich Swift Style Guide](https://github.com/raywenderlich/swift-style-guide)
- [StyleShare Swift Style Guide](https://github.com/StyleShare/swift-style-guide#%EC%B5%9C%EB%8C%80-%EC%A4%84-%EA%B8%B8%EC%9D%B4)
