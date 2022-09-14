# swift-style-guide

Apple Developer Academy의 개발자들이 따르고 있는 스위프트 스타일 가이드입니다. 다른 사람의 코드를 읽을 때 가독성을 높여주며,
내가 코드를 작성할 때 애매한 부분을 제거해줘 생산성 향상에 도움을 줍니다!

취향에 문제가 많기 때문에 코드를 작성하는데 어려움이 생긴다면 PR을 통해 언제나 의견을 주세요.

기여를 하고싶으신 분들을 위한 가이드는 [컨트리뷰션 가이드라인](./.github/CONTRIBUTING.md)을 참고해주세요.




## 목차

1. [네이밍](#네이밍)
    1. [변수](#변수)
    2. [함수](#함수)
    3. [열거형](#열거형)
    4. [구조체와 클래스](#구조체와-클래스)
    5. 델리게이트
2. [주석](#주석)
3. [띄어쓰기](#띄어쓰기)
4. 코드 구성
   1. 미사용 코드
5. 접근제어자
6. 클래스와 스트럭트
7. 함수호출
8. [클로져](#클로져)
    1. [다중 후행 클로져](#다중-후행-클로져)
9. 타입
    1. [타입 추론](#타입-추론)
    2. [타입 어노테이션](#타입-어노테이션)
10. [메모리 관리](#메모리-관리)


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
    - `request` : 에러가 발생하거나, 실패할 수 있는 비동기 작업에 사용합니다. 예를 들어, http 통신을 통해 값을 요청하는 경우가 이에 해당합니다.
    - `fetch` : 요청이 실패하지 않고 결과를 바로 반환할 때 사용합니다. 예를 들어, data를 찾고자 하는 모든 행위를 할 때가 이에 해당합니다.
    - **Good ✅**
        ```swift
        func reqeustData(for user: User) -> Data?
        func fetchData(for user: User) -> Data
        ```
    - **Bad ❌**
        ```swift
        func getData(for user: User) -> Data?
        ```
### 열거형
- 열거형의 이름은 `UpperCamelCase`를 사용해주세요.
- 열거형의 각 case에는 `lowerCamelCase`를 사용해주세요.
   - **Good ✅**
        ```swift
            enum Result {
              case .success
              case .failure
            }
        ```
    - **Bad ❌**
        ```swift
            enum result {
              case .Success
              case .Failure
            }
        ```
### 구조체와 클래스
- 구조체와 클래스의 이름은 `UpperCamelCase`를 사용해주세요.
- 구조체와 클래스의 프로퍼티 및 메소드는 `lowerCamelCase`를 사용해주세요.
   - **Good ✅**
        ```swift
            struct LeftRectangle {
                var width: Int
                var height: Int

                func drawRectangle() {
                    // ...
                }
            }
        ```
        ```swift
            class Mentee {
                let id: String
                let session: String
                var group: Int
                var team: Int

                func callOutMentor() {
                    // ...
                }
            }
        ```
    - **Bad ❌**
        ```swift
            struct rightRectangle {
                var Width: Int
                var Height: Int

                func DrawRectangle() {
                    // ...
                }
            }
        ```
        ```swift
            class mentor {
                let Id: String
                var Group: Int

                func GiveAdvice() {
                    // ...
                }
            }
         ```
## 주석
> 주석은 협업에 있어 가독성을 높이고 다른 사람의 코드를 이해하는 중요한 도구입니다. 
- 설명은 최대한 간결하고 핵심 요약에 집중해서 작성해주세요.
- 함수와 메소드는 기본적으로 무엇을 하는지 무엇을 반환하는지 설명해주시고,  
널효과나 void 반환은 생략합니다.
- 작성한 주석은 퀵헬프 메뉴에서 언제든지 조회가 가능합니다.

  - **Good ✅**
    ```swift
    /// 사용자 데이터를 추가합니다.
    /// - Parameter name: user fullname
    /// - Parameter age: user age
    func addData(name: String, age: Int) {
        // code to add data...
    }
    ```

    ```swift
    /// DB내 사용자 이름과 ID로 나이를 조회합니다.
    /// - Parameter ID: user ID
    /// - Parameter name: user fullname
    /// - Returns: user age
    func readData(ID: Int, name: String) {
        var age: Int
        // code to read data...
        return age
    }
    ```

  - **Bad ❌**
    ```swift
    // 사용자 데이터 추가
    func addData(name: String, age: Int) {
        // return void
    }
    ```

- 연관된 코드가 있다면 MARK를 사용하여 코드영역을 구분지는것을 권장합니다.  
  - **Example 💡**
      ```swift
      // MARK: - Gryffindor
      let password = "Fotuna Major"
      struct Gryffindor {
          let harry: String
          let ron: String
          let hermione: String
      }

      // MARK: - Slytherin  
      class Slytherin {
          let voldemort: String
          let malfoy: String
          func deadlyCurse() {
              print("Avada Kedavra!")
          }
      }
      ```

- 아직 개발이 완료되지 않은 코드가 있다면 TODO나 FIXME를 사용하여 체크하는 것도 좋습니다.
  - **Example 💡**
      ```swift
      // FIXME: - 버그 수정 필요
      public func buggyFunc() {
          // buggy code..
      }

      // TODO: - 문자열 인코딩 함수 작업 계획 
      private func todoFunc() {
          // tbd..
      }

## 들여쓰기
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
    
## 띄어쓰기
- 콜론(`:`)을 사용할 땐 콜론의 오른쪽으로 한 칸의 여백을 생성합니다. 콜론의 왼쪽은 공백없이 코드를 작성합니다.
  - **Example 💡**
    ```swift
    let leeo: HappyLeeo
    ```

## 클로져
### 다중 후행 클로져
- 함수 또는 메서드의 형식 매개변수에서 클로져들만을 실 매개변수로 받는 경우 함수 또는 메서드 호출 시 함수 또는 메서드의 소괄호, 첫 번째 실 매개변수의 라벨, 실 매개변수 사이의 콤마를 생략합니다.
  - **Good ✅**
    ```swift
    func doSomething(do: (String) -> Void, onSuccess: (Any) -> Void, onFailure: (Error) -> Void) {
        // function body
    }

    doSomething { something in
        // do closure
    } onSuccess: { result in
        // success closure
    } onFailure: { error in
        // failure closure
    }
    ```
  
  - **Bad ❌**
    ```swift
    func doSomething(do: (String) -> Void, onSuccess: (Any) -> Void, onFailure: (Error) -> Void) {
        // function body
    }

    doSomething (do: { something in
        // do closure
    }, onSuccess: { result in
        // success closure
    }, onFailure: { error in
        // failure closure
    })
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

## 메모리 관리
- 메모리 누수의 원인이 되는 순환 참조가 일어나지 않도록 주의해주세요.
- 객체 간의 관계를 분석하면서 `weak`와 `unowned`를 사용하여 순환 참조를 방지할 수 있습니다.
- `weak` 참조 변수는 반드시 Optional 타입이어야 합니다.
  - **Good ✅**
    ```swift
    class ExampleClass {
        weak var example: ExmapleClass? = nil
        
        init(){
            print("init class")
        }
        
        deinit{
            print("deinit class")
        }
    }

    // 객체 내의 인스턴스가 서로를 가리키고 있지만, weak 참조를 선언했기에 순환 참조가 일어나지 않습니다.
    var ex1: ExampleClass? = ExampleClass()
    var ex2: ExampleClass? = ExampleClass()

    ex1?.example = ex2
    ex2?.example = ex1

    ex1 = nil
    ex2 = nil

    // 출력결과
    // init class
    // init class
    // deinit class
    // deinit class
    ```

## Reference
- [Google Swift Style Guide](https://google.github.io/swift/)
- [Airbnb Swift Style Guide](https://github.com/airbnb/swift)
- [Linkedin Swift Style Guide](https://github.com/linkedin/swift-style-guide)
- [Raywenderlich Swift Style Guide](https://github.com/raywenderlich/swift-style-guide)
- [StyleShare Swift Style Guide](https://github.com/StyleShare/swift-style-guide#%EC%B5%9C%EB%8C%80-%EC%A4%84-%EA%B8%B8%EC%9D%B4)
