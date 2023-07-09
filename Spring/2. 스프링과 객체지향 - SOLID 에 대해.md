## SOLID란?
### 단일 책임 원칙 (Single responsibility principle)
+ 하나의 JSP문서에 View, Model(데이터접근), Query 가 모두 있는것은 이 법칙에 위배이다.
+ 하나의 클래스는 하나의 책임만을 져야한다.

### 개방/폐쇠 원칙 (Open/closed principle)
+ 소프트웨어의 확장에는 개방되어야 하나 변경에는 폐쇠되어야 한다.
+ 클라이언트가 역할을 수행함에있어 변경에 보수적이어야한다.

### 리스코프 치환 원칙 (Liskov substitution principle)
+ 객체는 프로그램의 정확성을 깨치지 않으면서 하위 타입의 인스턴스로 변경이 되어야 한다.
+ 예를들어 자동차의 엑셀기능을 구현한 구현체에서 뒤로가는 로직을 짜면 이는 **LSP를 지켰다고 할 수 없다.**

### 인터페이스 분리 원칙 (Interface segregation principle)
+ 인터페이스는 최소 단위로 분리되어야 한다.
+ 예를들어 자동차의 운전기능과 정비기능이 구현되어야 한다면 이 두가지를 다른 인터페이스로 분리하여 특정 클라이언트를 겨냥해야 한다.

### 의존관계 역전 원칙 (Dependency inversion principle)
+ 클라이언트는 구현 클래스보다 그 인터페이스에 의존해야 한다.
+ 역할과 구현을 분리하여야 한다 (다형성의 원칙)

## SOLID와 다형성의 역설
```
# 클라이언트
MemberService

# 인터페이스
MemberRepository

# 구현객체
MemoryMemberRepository - save()
JdbcMemberRepository - save()

------------------------------------
# 다형성이 지켜진 코드1
public class MemberService {
 	private MemberRepository memberRepository = new MemoryMemberRepository();
}

# 다형성이 지켜진 코드2
public class MemberService {
 // private MemberRepository memberRepository = new MemoryMemberRepository();
 	private MemberRepository memberRepository = new JdbcMemberRepository();
}
```
+ 자바의 다형성을 잘 지킨 위의 코드는 객체지향의 원칙에 위배하지 않았다고 말할 수 있을까?
+ 위 코드는 다형성이 지켜졌지만 기능 수행을 위해 클라이언트에서 직접 코드가 변경했기 때문에 **OCP를 지켰다고 할 수 없다.**
+ 위 코드는 클라이언트가 구현 클래스에 직접 접근하였기 때문에 **DIP를 지켰다고 할 수 없다.**
+ 다형성만으로는 쉽게 부품을 갈아끼우듯이 개발을 진행할 수 없고 클라이언트의 코드 또한 변경이 불가피하다.
+ 이를 해결하는 Spring의 어떠한 기능을 적용시켜야 한다.