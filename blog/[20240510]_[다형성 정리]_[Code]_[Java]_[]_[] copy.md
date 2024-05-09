### 다형성 정리

하나의 클래스에 

	public void ParentMethod () {
	System.out.println("Parent -> ParentMethod")
	}

또 다른 클래스에는

	public void ChildMethod () {
	System.out.println("Child -> ChildMethod") 
	}

메인 메서드는

	Parent poly = new Child 
	/* 이런식의 다형적 참조가 가능하다 
	부모 타입은 자식 타입을 담을 수 있지만 자식은 부모를 담을 수 없다 
	만약 poly.ChildMehtod();를 호출하고 싶다면 다운 캐스팅을 해야한다*/

다운 캐스팅 (부모타입 -> 자식타입) : 자식 타입으로 변경

	Child child = poly; // 이 경우 컴파일 에러 발생
	Child child = (Child) poly; // 다운캐스팅 (컴파일 에러X)
	// 이렇게 다운 캐스팅을 하면
	child.childMethod(); 를 할 수 있다

	- 일시적 다운 캐스팅 : 해당 메서드를 호출하는 순간만 일시적으로 다운 캐스팅
	((Child))poly  = child.childMethod(); // ()를 한번 더 선언하여 연산 우선자 우위

업 캐스팅 : 부모 타입으로 변경

	Child child= new Child();
	Parent parent1 = (Parent) Child; // 업캐스팅 -> 생략가능 오히려 권장
	Parent parent2 = Child; // 위의 코드와 동일 

캐스팅 주의사항

	Parent parent1 = new Child();  
	Child child1 = (Child) parent1;  
	child1.childMethod(); // 문제 x  
	Parent parent2 = new Parent();  
	Child child2 = (Child) parent2;  
	child2.childMethod(); // 메모리 자체에 Child 인스턴스가 존재 x

![[Pasted image 20240506230822.png]]
  
업캐스팅은 위험하지 않고 다운캐스팅만 위험한 이유 .jpg

- instanceof
- 출저 : 김영환 실전자바 기본편
```
public class CastingMain5 {  
    public static void main(String[] args) {  
        Parent parent1 = new Parent();  
        call(parent1);  
        Parent parent2 = new Child();  
        call(parent2);  
    }  
    private static void call(Parent parent) {  
        parent.parentMethod();  
        if (parent instanceof Child) {  
            System.out.println("Child 인스턴스 맞음");  
            Child child = (Child) parent;  
            child.childMethod();  
        } else {  
            System.out.println("child 인스턴스 아님");  
        }    
    }
}
```
	해석하기 어려운 경우 instanceof 키워드는 오른쪽 대상의 자식 타입을 왼쪽에서 참조하는
	경우에는 true를 반환한다 오른쪽 타입에 왼쪽에 있는 인스턴스의 타입이 들어갈 수 있는지
	대입해보면 된다 true면 가능 false면 불가능이라는 뜻이다
```

new Parent() instanceof Parent  
Parent p = new Parent() //같은 타입 true

new Child() instanceof Parent  
Parent p = new Child() //부모는 자식을 담을 수 있다. true

new Parent() instanceof Child

Child c = new Parent() //자식은 부모를 담을 수 없다. false new Child() instanceof Child

Child c = new Child() //같은 타입 true
```
마지막으로 다형성 메서드 오버라이딩을 할 때, 변수는 오버라이딩이 안되지만 메서드는 가능하다.