
### static
- 영어로 직역하면 '고정된'
- 클래스에 고정된 멤버로서 객체를 생성하지 않고 사용할 수 있는 필드와 메서드를 지정

##### 선언  
``` java
public class PlusClass{
  static int field1 = 15;

  static int plusMethod(int x, int y){ return x+y; } 
}
```
##### 활용 1
``` java
int ans1 = PlusClass.plusMethod(15,2);
int ans2 = PlusClass.field1 + 2; // 클래스 이름.필드로 사용 가능

PlusClass pc = new PlusClass(); // X 
int ans1 = pc.plusMethod(15,2); // X 이렇게 객체 참조 변수를 이용하는 것은 추천되지 않음
```

##### 활용 2
- 정적 메소드는 객체 참조 없이 바로 사용할 수 있는 특징 때문에 인스턴스 필드나 메소드, 그리고 this 키워드는 사용할 수 없음
**결국 JWT도 완벽한 기술은 아니나, 차선책은 될 수 있다.**  
#
hi
#


``` java
public class PlusClass{
  static int field1 = 15;
  int field2;

  void method1(){}
  static void method2(){}
  static int plusMethod(int x, int y){
    this.field2 = 10; // <-- x
    this.method1(); // <-- x
    field1 = 10; // <-- o
    method2(); // <-- o
  } 
}
```

**요약하자면 인스턴스 성질은 객체 생성 후 사용할 수 있으므로 객체 참조 없이 사용하는 정적 메소드에는 사용할 수 없음**

💡 static에서 파생된 디자인 패턴이 [싱글톤 패턴](https://astrid-dm.tistory.com/415)

***

### Final
- 영어로 직역하면 '최종의'
- 즉, 해당 변수는 값이 저장되면 최종적인 값이 되므로, 수정이 불가능

##### 선언
``` java
public class Shop{

  final int closeTime = 21; // final 필드에 값을 저장하는 방법 1 : 선언과 동시에 값을 줌
  final int openTime;

  public Shop(int openTime){ // final 필드에 값을 저장하는 방법 2 : 객체를 생성할 때 public Shop에 의해 값을 줌
    this.openTime = openTime;
  }
}
```
- 모든 가게의 오픈시간은 자유롭지만 한 번 정한 오픈시간은 바꿀 수 없고, 모든 가게가 21시에 문을 닫아야 할 때 위와 같이 `final` 키워드를 이용하면 오픈 시간은 객체마다 다르게 설정이 가능하지만, 닫는 시간은 고정하도록 설계가 가능

### static final
- 직역하면 '고정된 최종의 (값)'
- 상수(변하지 않는 값)를 선언하고자 할 때 사용됨
    - Final의 예시에서 언급된 코드를 보면, closeTime은 21시로 고정이지만 openTime은 객체마다 다를 수 있음을 보였다.
    - 그러나 openTime과 closeTime 모두 final로 선언되었는데, 절대 불변으로 고정된 closeTime의 경우 final 만으로는 부족하다는 특징을 가지고 있다.


##### static final 선언
``` java
static final double PI = 3.141592;
```
- static + final로 선언된 PI 값은 3.141592라는 불변의 값을 가짐
- 해당 값은 객체마다 저장될 필요가 없으며(static) + 여러 값을 가질 수 없음(final)


### 요약
|   |   |
|---|---|
|static|객체마다 가질 필요가 없는 공용으로 사용하는 필드. 또는, 인스턴스 필드를 포함하지 않는 메소드|
|final|한 번 값이 정해지면 바꿀 수 없는 필드|
|static final|모든 영역에서 고정된 값으로 사용하는 상수|
