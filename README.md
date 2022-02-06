# 자동차 경주 게임
## 진행 방법
* 자동차 경주 게임 요구사항을 파악한다.
* 요구사항에 대한 구현을 완료한 후 자신의 github 아이디에 해당하는 브랜치에 Pull Request(이하 PR)를 통해 코드 리뷰 요청을 한다.
* 코드 리뷰 피드백에 대한 개선 작업을 하고 다시 PUSH한다.
* 모든 피드백을 완료하면 다음 단계를 도전하고 앞의 과정을 반복한다.

## 온라인 코드 리뷰 과정
* [텍스트와 이미지로 살펴보는 온라인 코드 리뷰 과정](https://github.com/next-step/nextstep-docs/tree/master/codereview)

# 계산기

## 기능 구현 사항

- [X] 입력
- [X] 검증
  - [X] 숫자하고 계산기 특수문자(`+ * / -`)를 제외하면 오류 처리한다.
  - [X] 각 문자사이 공백은 한칸이다. 한칸이 넘으면 에러 처리한다.
  - [X] 입력인 `null`이거나 공백문자이면 `IllegalArgumentException throw`
  - [X] 사칙연산 기호가 아닌 경우 `IllegalArgumentException throw`
  - [X] 숫자 / 연산기호 순서가 올바르지 않을 경우 Parse 전용 `Exception throw` 출력 
- [X] 파싱
  - [X] 공식 파싱 검증 부분은 파싱 클라스가 담당
  - [X] 파싱해서 숫자, 사칙연산 기호 getter로 반환.
- [X] 계산
  - [X] 문자열 계산기는 사칙 연산의 계산 우선순위가 아닌 입력 값에 따라 계산 순서가 결정된다.
  - [X] 즉, 수학에서는 곱셈, 나눗셈이 덧셈, 뺄셈 보다 먼저 계산해야 하지만 이를 무시한다. 
  - [X] 예를 들어 `2 + 3 * 4 / 2`와 같은 문자열을 입력할 경우 `2 + 3 * 4 / 2` 실행 결과인 10을 출력해야 한다.
- [X] 결과 반환
- [x] 유닛테스트
  - 잘못된 formula
    - 공백 2칸 이상일때, IllegalArgumentException 발생한다.
      - [x] `2   + 3 * 4 / 2`
    - 숫자 연속 2개 올 때, IllegalArgumentException 발생한다.
      - [x] `2 3 * 4 / 2` 
    - 문자 연속 2개 올 때, IllegalArgumentException 발생한다.
      - [x] `+ + 3 * 4 / 2` 
    - 사칙 연산기호 아닌것일때 IllegalArgumentException 발생한다.
      - [x] `2 & 3 * 4 / 2`
    - null일때 IllegalArgumentException 발생한다.
      - [x] `null`
      - [x] ``
      - [x] ` `
  - [x] 정상 formula: `2 + 3 * 4 / 2` 일 때 의도한 값 `10`을 반환한다.

# 자동차 경주

## 기능 구현 사항

- [X] 주어진 횟수 동안 n대의 자동차는 전진 또는 멈출 수 있다.
- 입력
  - [X] 사용자는 자동차가 몇 대인지 입력 받을 수 있다.
    - `경주할 자동차 이름을 입력하세요(이름은 쉼표(,)를 기준으로 구분).`
  - [X] 사용자는 자동차가 몇 번의 이동을 할 것인지를 입력할 수 있어야한다.
    - `시도할 횟수는 몇 회인가요?`
- 자동차 이름
  - [X] 이름을 부여할 수 있다.
  - [X] 자동차의 이름은 5자를 초과할 수 없다.
  - [X] 자동차 이름은 쉼표(,)를 기준으로 구분한다.
- 전진
  - [X] 전진하는 자동차를 출력할 때 자동차 이름을 같이 출력한다.
  - [X] 0에서 9사이 무작위 값중 0~3은 제자리에, 4~9는 전진한다.
- [X] 자동차의 상태를 화면에 출력한다. 어느 시점에 출력할 것인지에 대한 제약은 없다.
- 결과
  - [X] 자동차 경주 게임을 완료한 후 누가 우승했는지 알려준다.
  - [X] 우승자는 한 명 이상일 수 있다.

## 추가 요구 사항

- [X] 모든 로직에 단위 테스트를 구현한다.
- [X] indent depth는 2를 넘지 않도록 한다.
- [X] else 예약어를 쓰지 않는다.
- [X] switch/case 예약어를 쓰지 않는다.
- [X] 함수의 길이가 15라인을 넘어가지 않도록 구현한다.

## 리펙토링 사항

- [x] 핵심 비즈니스 로직을 가지는 객체를 domain 패키지에 구현한다.
- [x] UI 관련한 객체를 view 패키지에 구현한다.
- [x] MVC 패턴 기반으로 리팩터링해 view 패키지의 객체가 domain 패키지 객체에 의존할 수 있지만, domain 패키지의 객체는 view 패키지 객체에 의존하지 않도록 구현한다.
- [x] 테스트 가능한 부분과 테스트하기 힘든 부분을 분리해 테스트 가능한 부분에 대해서만 단위 테스트를 진행한다.
- [x] setup() 조금 더 알맞은 위치 찾기.
- [x] mapToInt 활 용하기
- [x] Exception에 에러 메세지 넣기
- [x] RandomMovableStrategy 싱글톤 활용하기
- [x] startGame 테스트 작성하기
- [x] 상수 static final로 선언하기
- [x] Parser 객체 테스트 작성하기

## step2

- [ ] startGame()메서드는 static이여서 GameController객체가 필요없어 보인다. 인스턴스 객체를 만들어줄 필요가 있을지 고민해보자.
- [x] GameController의 cars, turn 맴버젼수에 대한 static 선언에 대해 고민해보자.
- [x] CarTest를 만들어보자.
- [x] name()와 distance() 메서드의 네이밍을 수정
  - JAVA는 메서드를 동사형으로 선언한다. 멤버변수에 대한 리턴은 get을 붙여서 해보자.
- [x] 팩토리메서드 vs 생성자를 통한 생성에 대해 고민해보자. (Cars Factory Method 적용)
- [x] 테스트코드의 패키지 위치는 프로덕션코드의 위치와 동일하게 맞추기

## 마감 기한

목요일 18시

## multiple authors

```bash
git commit -m "commit message


Co-authored-by: hochan222 <hochan049@gmail.com>
Co-authored-by: kworkbee <g1.tommy.jeon@gmail.com>"
```