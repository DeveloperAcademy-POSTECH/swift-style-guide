# swift-style-guide

Apple Developer Academy의 개발자들이 따르고 있는 스위프트 스타일 가이드입니다. 다른 사람의 코드를 읽을 때 가독성을 높여주며,
내가 코드를 작성할 때 애매한 부분을 제거해줘 생산성 향상에 도움을 줍니다!

취향에 문제가 많기 때문에 코드를 작성하는데 어려움이 생긴다면 PR을 통해 언제나 의견을 주세요.

기여를 하고싶으신 분들을 위한 가이드는 [컨트리뷰션 가이드라인](./.github/CONTRIBUTING.md)을 참고해주세요.




## 목차
1. [네이밍](#네이밍)
   1. [변수](#변수)
   2. [함수](#함수)
   3. 델리게이트
2. 코드 구성
   1. 미사용 코드
3. 접근제어자
4. 클래스와 스트럭트
5. 함수호출
6. 클로져
7. 타입
    1. [타입 추론](#타입-추론)
    2. [타입 어노테이션](#타입-어노테이션)
8. 메모리 관리


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
### 함수
- 함수 이름에는 `lowerCamelCase`를 사용해주세요.
- 함수는 일반적으로 동사원형으로 시작해주세요.
- Event-Handling 함수의 경우 (조동사 + 동사원형)으로 시작해주세요. 주어는 유추 가능하다면, 생략 가능합니다.
    - will은 특정 행위가 일어나기 직전을 의미합니다.
    - did는 특정 행위가 일어난 직후를 의미합니다.
    - **Good ✅**
        ```swift
        class AcademyViewController {

          private func didFinishSession() {
            // ...
          }

          private func willFinishSession() {
            // ...
          }

          private func scheduleDidChange() {
            // ...
        	}
        }
        ```
    - **Bad ❌**
        ```swift
        class AcademyViewController {

          private func handleSessionEnd() {
            // ...
          }

          private func finishSession() {
            // ...
          }

          private func scheduleChanged() {
            // ...
          }
        }
        ```
- 데이터를 가져오는 함수의 경우, `get` 사용을 지양하고 `request`, `fetch`을 적절하게 사용해주세요.
    - `request` : 에러가 발생하거나, 실패할 수 있는 비동기 작업에 사용합니다.
    - `fetch` : 요청이 실패하지 않고 결과를 바로 반환할 때 사용합니다.
    - **Good ✅**
        ```swift
        func reqeustData(for user: User) -> Data?
        func fetchData(for user: User) -> Data
        ```
    - **Bad ❌**
        ```swift
        func getData(for user: User) -> Data?
        ```

## 띄어쓰기
- 인덴테이션은 스페이스바 4개를 기본으로 하되, 스페이스바 4개는 탭 1개의 역할을 합니다.
  - **Good ✅**
      ```swift
      func sayHiLeeo(isHappy: Bool) {
          if isHappy {
              print("Hi Leeo!")
          }
      }
      ```
  - **Bad ❌**
      ```swift
      func sayHiLeeo(isHappy: Bool) {
        if isHappy {
          print("Hi Leeo!")
        }
      }
      ```

## 타입
### 타입 추론
- 컴팩트 코드를 선호하고 컴파일러가 단일 인스턴스의 상수나 변수의 타입을 추론하도록 합니다.
- 필요한 경우 `CGFloat`나 `Int64`와 같은 경우는 특정 타입을 지정해줍니다.
  - **Good ✅**
    ```swift
    let apple = "Developer"
    let book1 = Book()
    let age = 25
    let frameWidth: CGFloat = 120
    ```
  
  - **Bad ❌**
    ```swift
    let apple: String = "Developer"
    let book1: Book = Book()
    let age: Int = 25
    ```
    
### 타입 어노테이션    
- 전체 제네릭 구문 `Array<T>`와 `Dictionary<T: U>` 보다는 단축 구문 `[T]`, `[T: U]`를 사용합니다.
  - **Good ✅**
    ```swift
    var student: [String: String]?
    var students: [String]?
    ```
  
  - **Bad ❌**
    ```swift
    var student: Dictionary<String, String>?
    var students: Array<String>?
    ``` 

- 빈 배열과 딕셔너리 선언 시, 타입을 명시하는 것을 선호합니다.
  - **Good ✅**
    ```swift
    var student: [String: String] = [:]
    var students: [String] = []
    ```
  
  - **Bad ❌**
    ```swift
    var student = [String: String]()
    var students = [String]()
    ``` 

## Reference
- [Google Swift Style Guide](https://google.github.io/swift/)
- [Airbnb Swift Style Guide](https://github.com/airbnb/swift)
- [Linkedin Swift Style Guide](https://github.com/linkedin/swift-style-guide)
- [Raywenderlich Swift Style Guide](https://github.com/raywenderlich/swift-style-guide)
- [StyleShare Swift Style Guide](https://github.com/StyleShare/swift-style-guide#%EC%B5%9C%EB%8C%80-%EC%A4%84-%EA%B8%B8%EC%9D%B4)
