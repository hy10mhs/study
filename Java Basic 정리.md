[변수]
```Java
Class Variables {
    int instance_var; // 인스턴스 생성 후 접근 가능
    static int class_var; // 인스턴스 생성없이 접근 가능
    // 멤버변수 외에는 모두 지역변수
}
```

[메서드]
- parameter(부모) >= argument. 반환타입(부모) >= 반환값 // 다형성
- static 메서드는 같은 클래스 내 인스턴스 메서드를 호출할 수 없다
- 메서드가 인스턴스 변수 또는 메서드를 사용하지 않는 경우 static을 붙이자
- parameter 타입이 기본형일 때는 값 복사, 참조형인 경우 주소 복사

[오버로딩]
- 이름은 같으나 매개변수 개수 또는 타입이 다른 메서드를 정의
- 반환타입은 고려대상 아님

>가변인자를 사용하는 경우 가변인자는 제일 마지막 매개변수로 선언해야 한다. 그렇지 않으면 컴파일 에러 (가변인자인지 아닌지 구별할 방법이 없음). 가변인자에는 인자가 없어도 되고 배열도 인자가 될 수 있다 (가변인자는 내부적으로 배열을 사용한다; 호출 시 매번 배열을 새로 생성하는 비효율이 숨어있기 때문에 꼭 필요한 경우에만 사용하자). 가변인자가 아닌 배열로 매개변수를 선언한 경우에는 반드시 인자를 지정해 줘야하는 차이가 있다 (인자를 생략할 수 없으니 null이나 길이가 0인 배열을 넣어줘야 하는 불편함이 있다).

[생성자]
- 인스턴스 초기화 메서드
- new 연산자가 인스턴스를 생성하는 것이지 생성자가 인스턴스를 생성하는 것은 아니다.
- 기본생성자
  - 컴파일할 때, 생성자가 하나도 없는 경우 자동으로 추가된다. "클래스이름() {}"
  - 따라서, 생성자가 하나라도 정의되어 있는 경우에는 기본생성자는 생성되지 않는다.

- this()
  - 같은 클래스의 다른 생성자를 호출할 때 사용. 반드시 첫 줄에서만 사용가능.
    ```Java
    Car(String color) {
        this(color, "auto"); // 생성자도 오버로딩 가능
        door = 5;
    }
    ```
    
- this
  - 인스턴스 자신을 가리키는 참조변수, 모든 인스턴스 메서드에 지역변수로 숨겨진 채 존재 (static method에서는 this를 사용할 수 없음)
    ```Java
    Car(String color) {
        this.color = color;
    }
    ```

[변수초기화]
- 멤버변수(클래스 변수, 인스턴스 변수)와 배열의 초기화는 선택적이지만, 지역변수의 초기화는 필수적이다.
    ```Java
    boolean -> false
    char -> '\u0000'
    byte, short, int -> 0
    long -> 0L
    float -> 0.0f
    double -> 0.0d 또는 0.0
    참조형 변수 -> null
    ```
    
- 멤버변수의 초기화 방법
    - 명시적 초기화 (선언과 동시에 초기화)
        ```Java
        int door = 4;
        Engine e = new Engine());
        ```
    - 초기화 블럭
        ```Java
        인스턴스 초기화 블럭
        { /* 메서드처럼 조건/반복/예외처리 가능 */ }
        
        클래스 초기화 블럭
        static {}
        ```
    - 생성자
        
- 멤벼변수 초기화 시기와 순서
  - 클래스 변수
    - 시점: 클래스가 처음 로딩될 때 단 한번
    - 순서: 기본값 -> 명시적 초기화 -> 클래스 초기화 블럭
  - 인스턴스 변수
    - 시점: 인스턴스가 생성될 때 각 인스턴스마다
    - 순서: 기본값 -> 명시적 초기화 -> 인스턴스 초기화 블럭 -> 생성자
        
[상속]
- 생성자와 초기화 블럭은 상속되지 않고, 멤버(멤버변수 + 메서드)만 상속된다.
- 자손 클래스의 멤버 개수는 조상 클래스보다 항상 같거나 많다.
- 접근 제어자가 private 또는 default인 멤버들은 상속되지 않는다기보다 상속은 받지만 자손 클래스로부터의 접근이 제한된다
- 상속관계 vs 포함관계
  - 상속: -은 -이다. (is-a)
  - 포함: -은 -을 가지고 있다. (has-a)  
- 오버라이딩: 조상 클래스로부터 상속받은 메서드의 내용을 변경하는 것
  - 이름이 같고, 매개변수가 같고, 리턴타입이 같아야 한다.
  - 접근 제어자는 조상 클래스의 메서드보다 좁은 범위로 변경할 수 없다. (protected면 protected, public 가능)
  - 조상 클래스의 메서드보다 많은 수(넓은 범위)의 예외를 선언할 수 없다.
  - 인스턴스 메서드를 static 메서드로 또는 클래스 메서드를 인스턴스 메서드로 변경할 수 없다.
> 자손 클래스에서 동일한 이름, 매개변수, 리턴타입으로 static 메서드를 선언할 수 있으나 이것은 오버라이딩이 아닌 별개의 메서드를 선언한 것으로 '클래스이름.메서드이름()'으로 각각 호출.

- super
  - 조상 클래스로부터 상속받은 멤버를 참조하는데 사용하는 참조변수.
  - 조상 클래스로부터 상속받은 멤버도 자손 클래스의 멤버이므로 super대신 this를 사용할 수 있다.
  - 조상 클래스의 멤버(메서드 포함)와 자손클래스의 멤버가 중복 정의되어 서로 구별해야하는 경우에만 super를 사용하는 것이 좋다.
  - 모든 인스턴스 메서드에는 this, super가 존재한다. static 메서드에서는 this. super를 사용할 수 없다.

- super()
  - 조상 클래스의 생성자를 호출하는데 사용.
  - 자손 클래스의 인스턴스를 생성하면, 자손의 멤버와 조상의 멤버가 합쳐진 하나의 인스턴스가 생성된다.
  - 이 때, 자손 클래스의 생성자에서 조상 클래스의 생성자가 호출되어야 한다.
  - 생성자의 첫 줄에서 조상 클래스의 생성자를 호출하는 이유는 자손 클래스의 멤버가 조상 클래스의 멤버를 사용할 수도 있으므로 조상의 멤버가 먼저 초기화되어 있어야 하기 때문.
  - Object 클래스를 제외한 모든 클래스의 생성자는 첫 줄에 반드시 자신의 다른 생성자 또는 조상의 생성자를 호출해야 한다. 그렇지 않으면 컴파일러는 생성자 첫 줄에 super()를 자동으로 추가한다.

[package]
- 모든 클래스는 반드시 하나의 패키지에 속해야 한다.
- 한 소스파일에는 첫번째 문장으로 한 패키지 선언만 허용된다.
- 자신이 속한 패키지를 지정하지 않은 클래스는 자동적으로 이름 없는 패키지에 속하게 된다.

[import]
- import문은 프로그램 성능에 전혀 영향이 없다. 컴파일 시간이 아주 조금 더 걸릴 뿐.
- *을 사용하는 것이 하위 패키지의 클래스까지 포함하는 것은 아니다.
    ```
    java.* 는 java.util.*, java.text.* 를 포함하지 않는다.
    ```
- 같은 패키지 내 클래스들은 import문을 지정하지 않고도 패키지 명을 생략할 수 있다.
- import static으로 static 멤버를 호출할 때 클래스 이름을 생략할 수 있다.

[제어자]
- 사용가능한 제어자
  - 클래스: public, (default), final, abstract, static
  - 메서드: public, (default), protected, private, final, abstract, static
  - 멤버변수: public, (default), protected, private, final, static
  - 지역변수: final

- 접근 제어자
  - private: 같은 클래스
  - default: 같은 패키지
  - protected: 같은 패키지, 다른 패키지의 자손 클래스
  - public: 제한 없음
        
> 생성자가 private인 클래스는 조상이 될 수 없다. 자손 클래스의 인스턴스를 생성할 때 조상 클래스의 생성자를 호출해야 하는데, 생성자의 접근 제어자가 private이므로 자손 클래스에서 호출하는 것이 불가능하기 때문. 클래스 앞에 final을 추가해서 상속할 수 없는 클래스라는 것을 알리는 것이 좋다 (Math)
    
- final (대표적으로 String, Math)
  - 클래스: 상속할 수 없는 클래스가 된다.
  - 메서드: 오버라이딩 할 수 없다.
  - 멤버변수, 지역변수: 상수가 된다. (보통 선언과 동시에 초기화하지만, 인스턴스 변수의 경우 생성자에서 초기화할 수 있다)
> 메서드에 private과 final을 같이 사용할 필요는 없다. => private 메서드는 오버라이딩 불가능

- abstract
  - 클래스: 클래스 내 추상 메서드가 있음을 의미
  - 메서드: 선언부만 작성하고 구현부는 작성하지 않은 추상 메서드임을 알림.
> abstract은 static, final, private을 함께 쓰지 않는다.

[다형성]
- 업캐스팅: Parent parent = child (O)
- 다운캐스팅: Child child = parent (X) 형변환 생략불가
- 어떤 인스턴스의 instanceof 결과가 true인 것은 검사한 타입으로 형변환이 가능하다는 것을 의미한다.
> 조상 클래스의 메서드를 자손 클래스가 오버라이딩한 경우 참조변수의 타입에 관계없이 실제 인스턴스의 메서드(오버라이딩된 메서드)가 호출되지만, 멤버변수와 static 메서드는 참조변수의 타입에 영향을 받는다. 인스턴스 메서드만 영향을 받지 않는다

[추상클래스]
- 추상 클래스로는 인스턴스를 생성할 수 없다.
- 일부만 구현한다면 자손 클래스에 abstract를 붙여줘야 한다.
> 추상 메서드가 없는 클래스를 abstract를 붙여 추상 클래스로 만드는 경우도 있는데, 이런 클래스는 인스턴스를 생성해봐야 할 수 있는 것이 없어 인스턴스를 생성하지 못하게 막아둔 것이다. abstract없이 구현부만 안쓰면 별 차이없을 것 같지만, abstract를 붙여 자손 클래스에서 추상 메서드를 반드시 구현하도록 강제하는 데 의미가 있다.

[인터페이스]
- 일종의 추상클래스.
- 일부만 구현한다면 자손 클래스에 abstract를 붙여줘야 한다.
- 추상클래스와 달리 몸통을 가진 일반 메서드 또는 멤버변수를 가질 수 없다.
- 오직 추상메서드와 상수만을 멤버로 가질 수 있다.
    ```Java
    interface 인터페이스이름 {
        public static final 타입 상수이름 = 값;
        // 모든 멤버변수는 public static final, 생략가능
        
        public abstract 메서드이름(매개변수 목록);
        // 모든 메서드는 public abstract, 생략가능
        // 오버라이딩 메서드는 조상 메서드보다 넓은 범위의 접근 제어자를 사용해야하므로 자손 클래스의 메서드는 항상 public
        // java8부터 static 메서드와 디폴트 메서드 사용 가능
    }
    ```
    
- 인터페이스의 장점
  - 개발시간 단축: 인터페이스를 구현한 클래스가 작성될 때까지 기다리지 않고도 양쪽에서 동시에 개발을 진행할 수 있다.
  - 클래스들 간 관계를 맺어줄 수 있다: 상속관계에 있지 않고, 같은 조상 클래스를 가지고 있지 않은 클래스들 간 하나의 인터페이스를 공동 구현하도록 함으로써 관계를 맺어줄 수 있다.
    ```Java
    즉, 상속트리를 하나 더 만들 수 있다!!!!!!!!!!
    [GroundUnit -> Marine, SCV, Tank]
    [AirUnit -> DropShip]
    [Repairable -> SCV, Tank, DropShip]
    ```
  - 클래스간 직접적인 관계를 인터페이스를 이용해서 간접적인 관게로 변경하면, 한 클래스의 변경이 다른 클래스에 영향을 미치지 않게 할 수 있다. 단, 구현 클래스를 제공하는 쪽에서는 인터페이스를 구현해야 하고, 제공받는 쪽에서도 인터페이스를 사용해야 한다.

- 다중상속?
  - 주된 클래스 하나를 상속받고 나머지는 포함시킴
  - 다형성 활용을 위해 interface를 반드시 이용하자
    ```Java
    AS-IS
        public class TV {
            protected boolean power;
            public void power() { power != power; }
        }

        public class VCR {
            protected int counter;
            public void play() { // TAPE 재생 }
        }

        public class TVCR extends TV {
            private VCR vcr = new VCR();
            public void play () { vcr.play(); }
        }

    TO-BE
        public class TV {
            protected boolean power;
            public void power() { power != power; }
        }

        public class VCR implements IVCR {
            protected int counter;
            public void play() { // TAPE 재생 }
        }

        interface IVCR {
            public void play() { // TAPE 재생 }
        }

        public class TVCR extends TV implements IVCR {
            private VCR vcr = new VCR();
            public void play () { vcr.play(); }
        }
    ```

- 인터페이스를 이용한 다형성
  - 매개변수 및 리턴타입이 인터페이스라는 것은 메서드가 해당 인터페이스를 구현한 클래스의 인스턴스를 반환한다는 것을 의미
    ```Java
    interface Parser {
        public abstract void parse(String fileName);
    }

    class ParserManager {
        public static Parser getParser(String type) {
            if(type.equals("XML")) {
                return new XMLParser();
            } else {
                return new HTMLParser();
            }
        }
    }

    class XMLParser implements Parser {
        public void parse(String fileName) { }
    }

    class HTMLParser implements Parser {
        public void parse(String fileName) { }
    }

    AS-IS
        XMLParser xmlParser = new XMLParser();
    TO-BE
        Parser parser = new XMLParser();
        or
        Parser parser = ParserManager.getParser("XML");
    ```
  - default method
    - 여러 인터페이스의 디폴트 메서드간 충돌
      - 인터페이스를 구현한 클래스에서 디폴트 메서드를 오버라이딩해야 한다.
    - 디폴트 메서드와 조상 클래스의 메서드간 충돌
      - 조상 클래스의 메서드가 상속되고, 디폴트 메서드는 무시된다.
> 복잡하면 그냥 오버라이딩 해버리면 그만..

[예외처리]
- 자바에서는 런타임에 발생하는 오류를 에러와 예외 두가지로 구분했다 (컴파일 에러, 논리적 에러는 논외)
- '에러'는 OutOfMemeoryError, StackOverflowError와 같이 일단 발생하면 복구할 수 없는 심각한 오류이고
- '예외'는 발생하더라도 수습될 수 있는 비교적 덜 심각한 것이다.

- 에외 클래스의 계층구조
  ```
  Object> Throwable > Exception > IOException
                                > ClassNotFoundException
                                > FileNotFoundException
                                > DataFormatException 
                                > ...
                                > RuntimeException > ArithmeticException
                                                   > ClassCastExcepion
                                                   > NullPointerException
                                                   > ...
                                                   > IndexOutOfBoundsException
                    > Error     > OutOfMemeoryError
                                > ...
                                > StackOverflowError
    ```                            
- RuntimeException: 프로그래머 실수. 예외처리 강제 X(unchecked exception).
- Exception(RuntimeException 제외): 사용자 실수. 예외처리 강제 O(checked exception. 예외처리가 없으면 컴파일조차 되지 않음)
- throws에는 checked exception만 보통 씀 (unchecked exception을 써도 문제되지는 않지만)
- 예외가 발생한 경우 try -> catch -> finally, 예외가 발생하지 않은 경우 try -> finally
    catch에 적힌 예외클래스의 instanceof이 true면 catch 블럭 실행.
> 기존의 예외 클래스는 주로 Exception을 상속받아서 checked 에외로 작성하는 경우가 많았지만,요즘은 예외처리를 선택적으로 할 수 있도록 RuntimeException을 상속받아서 작성하는 쪽으로 바뀌어가고 있다. checked 예외는 반드시 예외처리를 해줘야 하기 때문에 예외처리가 불필요한 경우에도 try-catch를 넣어서 코드가 복잡해지기 때문이다. 프로그래밍 환경이 달라진 만큼 필수적으로 처리해야만 할 것 같았던 예외들이 선택적으로 처리해도 되는 상황으로 바뀌는 경우가 종종 발생하고 있다. 그래서 필요에 따라 예외처리의 여부를 선택할 수 있는 unchecked 예외가 강제적인 checked 예외보다 더 환영받고 있다.

[Collection Framework]
- List - 순서가 있다. 중복 허용 O.
  - ArrayList
    - Object 배열에 순차 저장. 공간이 없으면 새로운 배열에 복사 후 저장. 저장 개수를 고려해서 여유있는 크기로 생성하는 것이 좋다 (단, 너무 큰 배열은 공간낭비)
    - 배열 중간에 위치한 객체를 추가하거나 삭제하는 경우 데이터를 이동시켜줘야 하므로 시간이 오래 걸린다. 순차적으로 저장하거나 마지막 요소부터 삭제하는 것은 빠르다 (단, 배열 공간이 충분하다는 전제)
    - 한 요소가 삭제되면 빈 공간을 채우기 위해 뒤 요소들이 전진 이동한다 (둘 이상의 요소가 삭제될 수 있는 경우 뒤에서 부터 찾자)
  - LinkedList
    - 실제로는 더블 링크드 리스트로 구현되어 있음
  - 뭘 써야하나
    ```
                read        add/remove
    ArrayList    Win     순차적인 추가/삭제는 Win
    LinkedList                  Win
    ```
> ArrayList는 random access가 가능하나, LinkedList는 처음부터 차례대로 따라가야하므로 데이터가 많을수록 read 성능이 떨어짐
            
> 데이터가 크지 않다면 뭘 써도 사실 상관없음.. 데이터 개수가 변하지 않는 경우라면 ArrayList. 데이터 개수의 변경이 잦다면 LinkedList. 조합해서 사용하는 것도 좋은 방법! 처음 데이터를 저장할 때는 ArrayList를 사용하고 작업할 때는 LinkedList로 데이터를 옮겨서 작업하면 좋은 효율을 낼 수 있다.
```Java
ArrayList al = new ArrayList(100000);
for(int i=0; i<100000; i++) al.add(i+"");
LinkedList ll = new LinkedList(al)
for(int i=0; i<1000; i++) ll.add(500, "X");
```
- Queue
  - Stack은 LIFO이므로 ArrayList로 구현이 적합하며, Queue는 FIFO이므로 LinkedList로 구현이 적합
  - Queue는 인터페이스로 정의되어 있고, LinkedList가 실제로 Queue를 구현하고 있음; Queue queue = new LinkedList()
  - PriorityQueue
    - Queue 인터페이스 구현체 중 하나로 저장한 순서에 관계없이 우선순위가 높은 것부터 꺼낸다.
    - null은 저장할 수 없고, 저장하려고 하면 NPE가 난다.
    - 배열을 사용하며, 자료구조로 힙을 사용함
        
- Iterator, ListIterator (Enumeration; Iterator 구버전)
  - iterator()는 Collection 인터페이스에 정의된 메서드로 List, Set 인터페이스를 구현한 클래스에 사용할 수 있음
  - Map 인터페이스를 구현한 클래스는 iterator()를 직접 호출할 수 없고, keySet(), entrySet()과 같은 메서드를 통해 키와 값을 따로 Set()형태로 가져오고 iterator()를 호출할 수 있음
  - ListIterator는 양방향 이동이 가능한 Iterator. 단, ArrayList, LinkedList와 같이 List 인터페이스를 구현한 컬렉션에서만 사용할 수 있음

- Arrays
  - 배열을 다루는데 유용한 static 메서드 집합
  - 배열복사, 배열채우기, 정렬/탐색, 문자열 비교 및 출력, List로 변환

> Arrays.asList(Object... a)로 반환한 List에 추가, 삭제가 불가능하다. 저장된 내용의 변경은 가능하다. 크기를 변경할 수 있는 List가 필요한 경우 List list = new ArrayList(Arrays.asList(1,2,3));
        
- Comparator와 Comparable
  - Comparable 기본 정렬기준(보통 오름차순)을 구현하는데 사용
  - Comparator 기본 정렬기준 외에 다른 기준으로 정렬하고자할 때 사용
  - 역순으로 만들고 싶은 경우 compareTo 결과에 -1을 곱하는 compare 메서드를 만들자.
```Java
Arrays.sort(Object[] a) // 객체 배열에 저장된 객체가 구현한 Comparable에 의한 정렬
Arrays.sort(Object[] a, Comparator c) // 지정한 Comparator에 의한 정렬
```

- Set - 순서가 없다. 중복 허용 X. 이미 동일한 값이 있는 경우 저장에 실패하고 false 반환
  - HashSet
> load factor는 저장공간이 가득 차기 전에 미리 용량을 확보하기 위한 것으로 기본값은 0.75이며, 저장공간이 75%가 채워졌을 때 용량이 두 배로 늘어난다.

> 새로운 요소를 추가하기 전에 저장된 요소와 같은 것인지 판별하기 위해 equals(), hashCode()를 호출하기 때문에 eqauls()와 hashCode()를 목적에 맞게 오버라이딩해야 한다.
            
> hashCode() 다음 조건을 만족해야 한다.
> 1. equals 메서드에 사용된 멤버변수의 값이 바뀌지 않는 한 인스턴스의 해시코드는 변하지 않아야 한다.
> 2. 두 객체의 equals 결과가 true면 hashCode가 같아야 하고, false면 같거나 달라도 됨. 그러나, 컬렉션 성능(해싱)을 향상시키기 위해서는 다른 값을 반환하는 것이 좋다 (해시코드가 같다고 해서 equals 결과가 true인 것은 아니다.)

> hashCode는 1.8부터 추가된 hash() 메서드를 사용하자. Objects.hash(인스턴스 변수들...)
> String 클래스는 문자열의 내용을 해시코드로 만들어 내어 내용이 같은 문자열에 대한 해시코드는 같다.
> 반면 Object 클래스는 객체 주소로 해시코드를 만들어 내어 실행할 때마다 해시코드 값이 바뀔 수 있다.
            
  - TreeSet
    - 이진 검색 트리(레드블랙트리)를 사용.
    - 정렬/검색/범위검색에 높은 성능을 보이는 자료구조.
    - 추가시 저장위치를 찾아야 하고 삭제시 트리 일부를 재구성해야하므로 LinkedList보다 추가/삭제에 대한 비용이 크다. 그 대신 배열이나 LinkedList에 비해 검색과 정렬기능이 뛰어나다.

- Map - 순서가 없다. 키는 중복을 허용하지 않고 값은 중복을 허용. 이미 동일한 키가 있는 경우 덮어 씌움 (not extends Collection)
  - 검색에 관한 대부분의 경우 HashMap이 뛰어나다. 단, 정렬/범위검색이 필요한 경우에는 TreeMap을 쓰자
  - Vector, Hashtable은 쓰지말자.. 개선된 ArrayList, HashMap을 쓰자.

- Collections
  - Arrays가 배열에 관련된 메서드를 제공하는 것처럼, Collections는 컬렉션과 관련된 메서드를 제공한다.

[Generics]
- 다양한 타입의 객체들을 다루는 메서드에 사용
- 객체의 타입을 컴파일 시에 체크하기 때문에 객체의 타입 안정성을 높이고 형변환의 번거로움이 줄어든다
- 지네릭 클래스
    ```Java
    class Box<T> {
        ArrayList<T> list = new ArrayList<T>();

        void add(T item) { list.add(item); }
        T get(int i) { return list.get(i); }
        ArrayList<T> getList() { return list; }
        int size() { return list.size(); }
        public String toString() { return list.toString(); }
    }
    ```
    
    - 용어
      - Box<T>: 지네릭 클래스
      - Box: 원시 타입 (raw type)
      - T: 타입 변수 또는 타입 매개변수

    - 지네릭 타입을 지정하지 않고 사용하는 경우 Object로 간주. 에러는 아니지만 unchecked or unsafe operation 경고 발생.
    ```Java
    Box b = new Box();
    b.setItem("ABC");
    b.setItem(new Object());
    ```

    - 제약
      - static 멤버
        - 모든 객체에 동일하게 동작해야하는 static 멤버에 타입 변수 T를 사용할 수 없다.
        - static 멤버는 parameterized type과 관계없이 동일한 것이어야 하기 때문이다.
        - 즉, item이 static 멤버변수라고 했을 때, Box<Apple>.item과 Box<Grape>.item이 다를 수 없다.
      - 배열
        - 지네릭 타입의 배열 생성은 허용되지 않는다 (x) new T[10]
        - 참조변수를 지네릭 타입의 배열로 선언하는 것은 가능. (o) T[] arr
      - new, instanceof의 피연산자

    - 객체 생성
      - 반드시! 참조변수와 생성자에 대입된 parameterized type이 같아야 한다.
        ```Java
        Box<Apple> appleBox = new Box<Apple>();
        Box<Fruit> appleBox = new Box<Apple>(); // (x) 상속관계도 안됨
        Box<Apple> appleBox = new FruitBox<Apple>(); // (o) 지네릭 클래스의 타입이 상속관계에 있고, parameterized type이 같은 것은 괜찮다.
        Box<Apple> appleBox = new Box<>(); // (o) JDK1.7부터 생략가능

        Box<Fruit> fruitBox = new Box<Fruit>();
        fruitBox.add(new Fruit()); // (o)
        fruitBox.add(new Apple()); // (o) Fruit의 자손들은 이 메서드의 인자가 될 수 있다.
        ```

    - 제한 PECS
      - <? extends T> 상한 제한. T와 그 자손들만 가능 (여러 타입의 인터페이스를 구현하는 경우에는 &로 연결. T extends Fruit & Eatable)
      - <? super T> 하한 제한. T와 그 조상들만 가능
      - <?> 제한 없음. <? extends Object>와 동일

- 지네릭 메서드
  - 지네릭 클랙스에 정의된 타입 매개변수와 지네릭 메서드에 정의된 타입 매개변수는 별개의 것이다.
  - 같은 타입 문자 T를 사용한다해도 같은 것이 아니라는 것에 주의하자.

- 지네릭 타입의 형변환
  - 지네릭 타입과 넌지네릭 타입간 형변환은 항상 가능. 단, 경고.
    ```Java
    Box box = null;
    Box<Object> objBox = null;
    box = (Box)objbox; // (o)
    objbox = (Box<Object>)box; // (o)
    ```

  - 타입 매개변수가 다른 지네릭 타입간에는 불가능
    ```Java
    Box<Object> objBox = null;
    Box<String> strBox = null;
    objBox = (Box<Object>)strBox; // (x)
    strBox = (Box<String>)objBox; // (x)
    ```
  - 타입 매개변수 다형성을 쓰고 싶으면 extends, super를 사용하자.
    ```Java
    Box<? extends Fruit> fruitBox = new Box<Apple>(); // (o)
    ```

[Lambda]
- 람다식을 함수형 인터페이스로 참조하여 메서드의 매개변수 or 반환타입으로 주고 받을 수 있다
- 함수형 인터페이스에는 하나의 추상메서드만 정의되어 있어야 한다
- @FunctionalIntterface를 붙이면 컴파일러가 함수형 인터페이스를 올바르게 작성하였는지 확인해주므로 반드시 붙이자
- 람다식 내에서 참조하는 지역변수는 final이 붙지 않았어도 상수로 간주한다. 해당 지역변수는 람다식 내에서나 다른 어느 곳에서도 값을 변경할 수 없다. 반면, 인스턴스 변수는 변경할 수 있다
- java.util.function
  - 매개변수 0개
    - java.lang.Runnable      void run()
    - Supplier<T>             T get()
  - 매개변수 1개
    - Consumer<T>             void accept(T t)
    - Function<T,R>           R apply(T t)
    - Predicate<T>            boolean test(T t)
  - 매개변수 2개
    - BiConsumer<T,U>         void accept(T t, U u)
    - BiFunction<T,U,R>       R apply(T t, U u)
    - BiPredicate<T,U>        boolean test(T t, U u)
  - 매개변수 3개가 필요한 경우에는 직접 만들어서 사용해야 한다
    ```Java
    @FunctionalIntterface
    interface TriFunction<T,U,V,R> {
        R apply(T t, U u, V v);
    }
    ```
  - 매개변수타입 = 반환타입
    - UnaryOperator<T>        T apply(T t)
    - BinaryOperator<T>       T apply(T t, T t)
  - 기본형 사용
    - DoubleToIntFunction     int apply(double d)
    - ToIntFunction           int applyAsInt(T value)
    - intFunction             R apply(int value)
    - ObjIntConsumer          void accpet(T t, int i)
  - 함수형 인터페이스의 default, static 메서드
    ```Java
    default <V> Function<T,V> andThen(Function<? super R, ? extends V> after)
    default <V> Function<V,R> compose(Function<? super V, ? extends T> before)
    static <T> Function<T,T> identity()

    default Predicate<T> and(Predicate<? super T> other)
    default Predicate<T> or(Predicate<? super T> other)
    default Predicate<T> negate()
    static <T> Predicate<T> isEqual(Object targetRef)
    ```
  - 메서드 참조
    - 하나의 메서드만 호출하는 람다식은 '클래스이름::메서드이름' or '참조변수::메서드이름'으로 바꿀 수 있다
    ```Java
    ClassName::method (static or 인스턴스 메서드 참조)
    obj::method (특정 객체의 메서드 참조)
    ```
  - 생성자를 호출하는 람다식도 메서드 참조로 변환할 수 있다. () -> new MyClass() / MyClass::new
  - 매개변수 개수에 따라 알맞은 함수형 인터페이스를 사용하면 된다. (i, s) -> MyClass::new

[Stream]
- 스트림은 데이터 소스를 변경하지 않는다.
- 스트림은 1회용이다. Iterator로 컬렉션의 요소를 모두 읽고 나면 다시 사용할 수 없는 것처럼 스트림도 한번 사용하면 닫혀서 다시 사용할 수 없다.
- 오토박싱 & 언박싱의 비효율을 줄이기 위해 기본형을 다루는 스트림이 있다 (IntStream, LongStream, DoubleStream)
- Stream 만들기
  - 컬렉션: Colllection.stream()
  - 배열: Stream.of(T... value), Stream.of(T[]), Arrays.stream(T[]), Arrays.stream(T[] array, int startInclusive, int endExclusive)
  - 기본형 스트림
    - IntStream.of(int... value), IntStream.of(int[]), Arrays.stream(int[]), Arrays.stream(int[] array, int startInclusive, int endExclusive)
    - IntStream.range(int begin, int end)
    - IntStream.rangeClosed(int begin, int end) // 경계포함
    - new Random().ints().limit(5) // ints()는 무한 스트림이므로 스트림 크기를 제한해주어야 한다.
    - new Random().ints(5)
    - new Random().ints(1,5) // 난수범위 1,2,3,4
  - 람다식 (무한 스트림)
    - Stream.iterate(0, n -> n+2) // 0, 2, 4, 6, ... 이전 결과를 다음 계산에 사용
    - Stream.generate(Math::random) // 이전 결과를 다음 계산에 사용하지 않음
- Stream 연결
  - Stream.concat(Stream.of(...), Stream.of(...))
- Stream 중간연산 (연산 결과가 스트림. 최종연산 전까지 중간연산은 수행되지 않는다; lazy)
  - skip() // 건너뛰기
  - limit() // 자르기
  - filter()
  - distinct()
  - sorted()
  - map()
  - peek() // 조회. 스트림의 요소를 소모하지 않으므로 연산 사이에 여러 번 끼워 넣어도 문제되지 않는다.
  - mapToInt(), maptoLong(), mapToDouble() // 기본형 스트림으로 변환
  - sum(), average(), max(), min(), summaryStatistics()
  - mapToObj(), boxed()
  - flatMap()
    ```Java
    1.
    Stream<String[]> arrStrm = Stream.of(
        new String[]{"a", "b", "c"},
        new String[]{"d", "e", "f"}
    );

    Stream<Stream<String>> strmStrm = arrStrm.map(Arrays::stream);
    Stream<String> strStrm = arrStrm.flatMap(Arrays::stream);

    2.
    String[] lineArr = {
        "Believe or not It is true",
        "Do or do not There is no try",
    };

    Stream<String> strm = Arrays.stream(lineArr);
    Stream<Stream<String>> strmStrm = strm.map(line -> Stream.of(line.split(" ")));
    Stream<String> strStrm = strm.flatMap(line -> Stream.of(line.split(" ")));

    3.
    Stream<String> strStrm = Stream.of("a","b","c");
    Stream<String> strStrm2 = Stream.of("d","e","f");
    Stream<Stream<String>> strmStrm = Stream.of(strStrm, strStrm2);
    Stream<String> strm = strmStrm
        .map(s -> s.toArray(String[]::new))
        .flatMap(Arrays::stream);
    ```
            
- Stream 최종연산 (연산 결과가 스트림이 아님. 단 한번 가능)
    ```Java
    void forEach(Consumer<? super T> action)
    boolean allMatch(Predicate<? super T> predicate)
    boolean anyMatch(Predicate<? super T> predicate)
    boolean noneMatch(Predicate<? super T> predicate)
    Optional<T> findFirst()
    Optional<T> findAny() // 병렬 스트림인 경우 findAny를 사용해야 한다.
    
    long count()
    Optional<T> max(Comparator<? super T> comparator)
    Optional<T> min(Comparator<? super T> comparator)

    Optional<T> reduce(BinaryOperator<T> accumulator) // 처음 두 요소로 연산한 결과를 가지고 다음 요소와 연산한다.
    T reduce(T identity, BinaryOperator<T> accumulator) // 초기값과 스트림의 첫번째 요소를 연산의 시작으로 한다. 스트림의 요소가 하나도 없는 경우 초기값을 반환하므로 반환 타입이 Optional<T>가 아닌 T이다.
    R collect(Collector collector)
    ```

    - R collect(Collector collector)
      - sort할 때 Comparator가 필요한 것처럼, collect할 때 매개변수로 Collector가 필요.
      - Collectors (static 메서드로 Collector 인터페이스의 구현체를 제공)
        - 스트림을 컬렉션과 배열로 반환
          - toList, toSet
          - toMap // Key,Value 지정 필요. toMap(Product::getId, Function.identity())
          - toCollection // 생성자 참조를 매개변수로 넣어줘야 함. toCollection(ArrayList::new)
          - toArray // 생성자 참조를 매개변수로 넣어줘야 함. toArray(Student[]::new)
        - 통계
          - counting()
          - summingInt()
          - averagingInt()
          - maxBy()
          - minBy()
        - 리듀싱
          - reducing()
        - 문자열 결합
          - joining()
        - 분할
          - Collector partitioningBy(Predicate predicate)
          - Collector partitioningBy(Predicate predicate, Collector downstream)
          - Collector groupingBy(Function classifier)
          - Collector groupingBy(Function classifier, Collector downstream)
          - Collector groupingBy(Function classifier, Supplier mapFactory, Collector downstream)
          - 결과는 Map에 담긴다.
          - partitioningBy가 빠르므로 Predicate으로 가능하면 partitioningBy를 사용하자
```Java
Map<Boolean, List<Student>> stuBySex = stuStream.collect(partitioningBy(Student::isMale));
List<Student> maleStudents = stuBySex.get(true);
List<Student> femaleStudents = stuBySex.get(false);

Map<Boolean, Long> stuNumBySex = stuStream.collect(partitioningBy(Student::isMale, counting()));
stuNumBySex.get(true); // 남학생 수
stuNumBySex.get(false); // 여학생 수

Map<Boolean, Optional<Student>> topScoreBySex = stuStream.collect(partitioningBy(Student::isMale, maxBy(comparingInt(Student::getScore))));
topScoreBySex.get(true); // 최고점수를 가진 남학생
topScoreBySex.get(false); // 최고점수를 가진 여학생

Map<Boolean, Map<Boolean, List<Student>>> failedStuBySex = stuStream.collect(
    partitioningBy(Student::isMale,
        partitioningBy(s -> s.getScore() < 150)
    )
);
List<Student> failedMaleStu = failedStuBySex.get(true).get(true);
List<Student> failedFemaleStu = failedStuBySex.get(false).get(true);                        
    
Map<Integer, List<Student>> stuByClassRoom = stuStream.collect(groupingBy(Student::getClassRoom)); // 기본적으로 List<T>에 담는다.
Map<Integer, List<Student>> stuByClassRoom = stuStream.collect(groupingBy(Student::getClassRoom, toList()));
Map<Integer, HashSet<Student>> stuByClassRoom = stuStream.collect(groupingBy(Student::getClassRoom, toCollection(HashSet::new)));
Map<Student.Level, Long> stuByLevel = stuStream.collect(groupingBy(s -> {
    if(s.getScore() >= 200) return Student.Level.HIGH;
    else if(s.getScore() >= 100) return Student.Level.MID;
    else return Student.Level.LOW;
}, counting()));
Map<Integer, Map<Integer, List<Student>>> stuByHakAndBan = stuStream
.collect(groupingBy(Student::getHak,
    groupingBy(Student::getBan)
));
```

[Optional]
```Java
pulbic final class Optional<T> {
    private final T value;
}
```
- Optional 생성
  - of, ofNullable: 참조변수의 값이 null일 가능성이 있으면, ofNullable을 사용해야 한다. of를 사용하면 NPE.
  - empty: 참조변수를 기본값으로 초기화할 때. 내부적으로 null을 저장하고 있다.
- Optional value
  - get: 값이 null이면 NoSuchElementException이 발생한다
  - orElse: 이 때를 대비해서 orElse()로 값을 지정할 수 있다
  - orElseGet: orElse 변형으로 null을 대체할 값을 반환하는 람다식을 지정할 수 있음
  - orElseThrow: orElse 변형으로 null일 때 지정된 예외를 발생시킬 수 있음
- filter, map, flatMap
  - map의 결과가 Optional<Optional<T>>일 때, flatMap을 사용하면 Optional<T>를 결과로 얻는다.
  - 만일 Optional 객체의 값이 null이면, 이 메서드들은 아무 일도 하지 않는다.
- isPresent
  - Optional 객체의 값이 null이면 false를, 아니면 true를 반환한다.
- ifPresent
  - 값이 있으면 주어진 람다식을 실행하고, 없으면 아무 일도 하지 않는다.

[Thread]
- 프로세스: 실행 중인 프로그램. OS로부터 실행에 필요한 자원(메모리)을 할당받아 프로세스가 실행됨
- 쓰레드: 프로세스에는 최소한 하나 이상의 쓰레드가 존재하며, 실제로 작업을 수행하는 주체이다
- 멀티쓰레딩: 하나의 프로세스에서 여러 쓰레드를 동시에 수행하는 것. CPU 코어가 한번에 단 하나의 작업을 할 수 있으므로 실제로 동시에 처리되는 작업의 개수는 코어의 개수와 일치한다.
- 쓰레드의 실행시간은 굉장히 불확실
  - JVM과 OS 종류에 따라 실행시간은 달라진다
    - JVM에 의해 어떤 쓰레드가 얼마동안 실행될지 결정되며
    - OS 프로세스 스케줄러에 의해 어떤 프로세스가 얼마동안 실행될지 결정된다
- 멀티쓰레딩의 장점
  - CPU 사용률을 향상시킨다
  - 자원을 보다 효율적으로 사용할 수 있다
  - 사용자에 대한 응답성이 향상된다
> But, 여러 쓰레드가 같은 프로세스 내에서 자원을 공유하면서 작업을 하기 때문에 발생할 수 있는 동기화, 데드락과 같은 문제들을 고려해줘야 한다
- 싱글쓰레드와 멀티쓰레드
  - 멀티쓰레드가 싱글쓰레드보다 더 느릴 수 있다.
    - context switching에 시간이 걸리기 때문에 (현재 진행 중인 작업의 상태, 에를 들면 PC 프로그램 카운터)
    - 프로세스의 스위칭은 더 많은 시간이 걸린다 (더 많은 정보가 불러지고 저장되어야 하므로)
    - 멀티쓰레드가 같은 자원을 공유하면 병목이 되어 느릴 수 있다.    
    - 그래서 단순히 "CPU만을 사용하는 계산" 작업이라면 오히려 멀티쓰레드보다 싱글쓰레드로 프로그래밍 하는게 더 효율적이다.
  - 멀티쓰레드가 서로 다른 자원을 사용하는 경우 멀티쓰레드가 싱글쓰레드보다 더 빠를 수 있다.
    - 사용자로부터 데이터를 입력받는 작업
    - 네트워크로 파일을 주고받는 작업
    - 프린터로 파일을 출력하는 작업

- 쓰레드 구현
  - Thread 클래스를 상속
    ```Java
    class MyThread extends Thread() {
        @Override
        public void run() [ ]
    }

    MyThread thread = new MyThread();
    thread.start();
    ```
  - Runnable 인터페이스를 구현
    ```Java
    class MyThread implements Runnable {
        @Override
        public void run() { }
    }

    Runnable r = new MyThread();
    Thread thread = new Thread(r);
    thread.start();
    ```
  - 어느 방법을 선택해도 상관없으나 Thread를 상속받으면 다른 클래스를 상속받을 수 없기 때문에 보통 Runnable 인터페이스를 구현한다.
  - Thread 클래스를 상속받으면 자손 클래스에서 조상인 Thread 클래스의 메서드를 직접 호출할 수 있지만, Runnable을 구현하면 Thread 클래스의 static 메서드인 currentThread()를 호출하여 쓰레드에 대한 참조를 얻어 와야만 가능하다
    ```Java
    class Thread1 extends Thread {
        public void run() {
            for (int i=0; i < 5, i+=) {
                System.out.println(getName()); // Thread를 상속받았기 때문에 간단히 getName()만 호출하면 된다.
            }
        }
    }

    class Thread2 implements Runnable {
        public void run() {
            for (int i=0; i < 5, i+=) {
                System.out.println(Thread.currentThread().getName());
            }
        }
    }
    ```
- 쓰레드 실행
  - thread.start();
    - 바로 실행되지는 않는다. 일단 대기상태에 있다가 자신의 차례가 되어야 실행된다. 다만 실행대기중인 쓰레드가 하나도 없으면 곧바로 실행된다.
    - 한 번 실행되어 종료된 쓰레드는 다시 실행할 수 없다.
    - 하나의 쓰레드 당 start()는 오직 한번만 실행될 수 있다.
  - main 쓰레드
    - main 메서드의 작업을 수행하는 것도 쓰레드이며, 이를 main 쓰레드라고 한다.
    - main 메서드가 수행을 마치더라도 프로그램이 종료되지 않을 수 있다.
    - 실행 중인 사용자 쓰레드가 하나도 없을 때 프로그램은 종료된다.      
- 쓰레드의 우선순위 필드를 사용하는 것은 비추!
  - 자바는 쓰레드의 우선순위에 대한 정책을 JVM에 강제하지 않고 강제하더라도 OS마다 스케줄링이 다를 수 있다.
  - 따라서, PriorityQueue에 넣고 우선순위가 높은 작업부터 먼저 처리하는게 나을 수 있다.
- 쓰레드 그룹
> 폴더 같은 개념으로 쓰레드 그룹 안에 다른 쓰레드 그룹을 둘 수 있다. 보안상 이유로 도입된 것으로, 자신이 속한 쓰레드 그룹이나 하위 쓰레드 그룹은 변경할 수 있지만 다른 쓰레드 그룹의 쓰레드를 변경할 수는 없다. 모든 쓰레드는 반드시 쓰레드 그룹에 포함되어 있어야 하기 때문에, 쓰레드 그룹을 지정하지 않은 쓰레드는 자신을 생성한 쓰레드와 같은 쓰레드 그룹에 속하게 된다. 자바 어플리케이션이 실행되면, JVM은 main과 system이라는 쓰레드 그룹을 만들고 JVM 운영에 필요한 쓰레드들을 생성해서 이 쓰레드 그룹에 포함시킨다. 예를 들어 main 메서드를 수행하는 main이라는 이름의 쓰레드는 main쓰레드 그룹에 속하고, 가비지컬렉션을 수행하는 Finalizer쓰레드는 system쓰레드 그룹에 속한다. 우리가 생성하는 모든 쓰레드 그룹은 main쓰레드 그룹의 하위 스레드 그룹이 되며, 쓰레드 그룹을 지정하지 않고 생성한 쓰레드는 자동으로 main쓰레드 그룹에 속하게 된다.
- 참조변수 없이 쓰레드를 생성해서 바로 실행시키더라도, 가비지 컬렉션 대상이 되지 않는다. 쓰레드의 참조가 쓰레드 그룹에 저장되기 때문에
    ```Java
    new Thread(threadGroup, r, "th1").start();
    new Thread(r, "th2).start();
    ```
- 데몬쓰레드
  - 일반쓰레드의 작업을 돕는 보조적인 역할
  - 일반쓰레드가 모두 종료되면 데몬 쓰레드는 강제적으로 자동종료된다.
  - 가비지 컬렉터, 워드프로세서의 자동저장, 화면자동갱신 등
  - 데몬쓰레드는 무한루프와 조건문을 이용해서 실행 후 대기하고 있다가 특정 조건이 만족되면 작업을 수행하고 다시 대기하도록 작성한다.
  - 일반쓰레드와 작성방법 및 실행방법은 같고, 실행전에 setDaemon(true)을 호출하기만 하면 된다.
  - 데몬쓰레드가 생성한 쓰레드는 자동으로 데몬쓰레드가 된다.

- 쓰레드의 상태
  - NEW: 쓰레드가 생성되고 아직 start()가 호출되지 않은 상태
  - RUNNABLE: 실행 중 또는 실행 가능한 상태
  - BLOCKED: 동기화 블럭에 의해서 일시정지된 상태(lock이 풀릴 때까지 기다리는 상태)
  - WAITING, TIMED_WAITING: 쓰레드의 작업이 종료되지는 않았지만 실행가능하지 않은 (unrunnable) 일시정지상태. TIMED_WAITING은 일시정지시간이 지정된 경우를 의미.
  - TERMINATED: 쓰레드의 작업이 종료된 상태
  - 상태변경
    - sleep() __static__
      - 일정시간동안 쓰레드를 멈추게 한다.
      - 지정된 시간이 다 되거나 interrupt()가 호출되면, InterruptedException이 발생되어 잠에서 깨어나 실행대기 상태가 된다.
      - 그래서 sleep()을 호출할 때는 항상 try-catch문으로 예외를 처리해줘야 한다.
      - 매번 예외처리를 해주는 것이 번거롭기 때문에, 아래와 같이 try-catch문까지 포함하는 새로운 메서드를 만들어 사용하기도 한다.
        ```Java
        void delay(long millis) {
            try {
                Thread.sleep(millis)
            } catch (InterruptedException e) { }
        }
        ```
      - 항상 실행 중인 쓰레드에 대해 작동하기 때문에 "참조변수.sleep()"을 해도 영향받는 쓰레드는 참조변수의 쓰레드가 아닌 현재 실행 중인 쓰레드이다.
      - 그래서 sleep()은 static으로 선언되어 있으며 참조변수로 호출하기 보다는 Thread.sleep()과 같이 해야 한다.
    - interrupt()
      - void interrupt()
        - 쓰레드의 interrupted상태를 false에서 true로 변경.
        - 단, 해당 쓰레드가 sleep(), wait(), join()에 의해 일시정지 상태(WAITING)에 있을 때에는 쓰레드의 상태는 false가 되고
        - sleep(), wait(), join()에서 InterruptedException이 발생하고 실행대기상태(RUNNABLE)로 바뀐다.
      - boolean isInterrupted()
        - 쓰레드의 interrupted상태를 반환
      - static boolean interrupted()
        - 현재 쓰레드의 interrupted상태를 알려주고, false로 초기화
      - "참조변수.interrupt(), 참조변수.isInterrupted()"는 참조변수가 가리키는 쓰레드 대상
      - "Thread.interrupted()"는 현재 쓰레드 대상
    - suspend(), resume(), stop()
      - Deprecated. 쓰지말자
    - yield() __static__
      - 다른 쓰레드에게 양보한다.
      - busy-waiting 상태가 될 쓰레드에서 yield()를 호출하면 다른 쓰레드에게 실행시간을 양보해서 효율을 높일 수 있다.
    - join()
      - 다른 쓰레드의 작업을 기다린다.
      - 시간을 지정하지 않으면 해당 쓰레드가 작업을 모두 마칠 때까지 기다리게 된다.
      - 작업 중에 다른 쓰레드의 작업이 먼저 수행되어야할 필요가 있을 때 사용하자.
      - sleep()처럼 interrupt()에 의해 대기상태에서 벗어날 수 있으며, join()이 호출되는 부분을 try-catch문으로 감싸야 한다.
      - sleep()과 다르게 현재 쓰레드가 아닌 참조변수가 가리키는 쓰레드에 대해 동작한다.
    
- 쓰레드의 동기화
  - 공유 데이터를 사용하는 코드 영역을 임계영역(critical section)으로 지정해놓고, 공유 데이터가 가지고 있는 lock을 획득한 단 하나의 쓰레드만 이 영역 내의 코드를 수행할 수 있도록 한다.
  - 해당 쓰레드가 임계영역 내의 모든 코드를 수행하고 벗어나서 lock을 반납해야 다른 쓰레드가 lock을 획득하여 임계영역의 코드를 수행할 수 있게 된다.
  - synchronized, JDK1.5부터는 java.util.concurrent.locks와 java.util.concurrent.atomic 패키지를 통해서 다양하게 동기화를 구현할 수 있다.
    ```Java
    public synchronized void method() {
        // 메서드 전체가 임계영역이 된다.
    }

    instance 메서드에 사용되면 해당 인스턴스의 한 쓰레드만 실행 가능하다는 의미.
    static 메서드에 사용되면 해당 클래스의 한 쓰레드만 실행 가능하다는 의미 (인스턴스 개수와 관계없이).
    
    public void method() {
        synchronized (this) { // monitor 객체당 하나의 쓰레드만 임계영역을 실행할 수 있다.
            // 임계영역
        }
    }

    public static void method() {
        synchronized (SynchronizedClass.class) { // moniotor 클래스당 하나의 쓰레드만 임계영역을 실행할 수 있다.
            // 임계영역
        }
    }
    ```
> synchronized는 지정된 영역의 코드를 한 번에 하나의 쓰레드가 수행하는 것을 보장하는 것이기 때문에 안에서 사용되는 변수가 public 할 경우 해당 코드 영역외에 다른 곳에서 변경되는 것을 막을 수 없다.
> 그래서 private으로 클래스 밖의 다른 곳에서의 변경을 차단하는 것이 좋다.

  - wait(), notify()
    - synchronized로 동기화해서 공유 데이터를 보호하는 것도 중요하지만, 특정 쓰레드가 락을 가진 상태로 오랜 시간 보내지 않도록 하는 것도 중요하다.
    - 임계영역을 진행하다가 더 이상 진행할 상황이 아니라면 일단 wait()을 호출해서 쓰레드가 락을 반납하고 기다리게 한다. 그러면 다른 쓰레드가 락을 얻어 작업을 수행할 수 있다.
    - 나중에 작업을 진행할 상황이 되면 notify()를 호출해서 작업을 중단했던 쓰레드가 다시 락을 얻어 작업을 진행할 수 있도록 한다.
    - 다만, 오래 기다린 쓰레드가 락을 얻는다는 보장은 없다.
    - wait()이 호출되면 실행 중이던 쓰레드는 waiting pool에서 기다린다. notifiy()가 호출되면 waiting pool에 있던 모든 쓰레드 중 임의 쓰레드 하나만 통지를 받는다.
    - notifiyAll()은 기다리고 있는 모든 쓰레드에게 통보되지만, 그래도 lock을 얻을 수 있는 것은 한 쓰레드일 뿐이고(race condition) 나머지 쓰레드는 통보를 받았어도 lock을 얻지 못하면 다시 lock을 기다리는 상태가 된다 (starvation).
    - 매개변수가 있는 wait은 지정된 시간동안만 기다린다.
    - waiting pool은 객체마다 존재하는 것이기 때문에 notifiyAll()이 모든 객체의 waiting pool에 있는 쓰레드까지 깨우는 것은 아니다.
    - synchronized 안에서만 사용할 수 있다.

[기타]
```Java
Tv[] tvArr = new Tv[3]; // tvArr -> {null, null, null}
tvArr[0] = new Tv(); // 객체 생성은 따로 해줘야 한다
```
- 생성자 또는 메서드를 사용하지 못하게 하려는 경우 (ex: abstract 클래스를 구현하면서 일부 메서드를 사용 못하게 막으려는 경우) 호출하는 쪽에서 제대로 동작하지 않는 이유를 알 수 있도록 메서드에서 에외를 던져주자 (ListIterator의 remove 메서드)


