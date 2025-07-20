## 🚀 객체 지향 프로그래밍 (OOP) 핵심 개념 총정리 및 코드 예시 🚀

OOP는 프로그램을 **객체** 단위로 설계하여 데이터 관리와 코드의 유연한 재사용, 확장을 돕는 프로그래밍 패러다임입니다.

---

### 1. 🏗️ 추상화 (Abstraction)

**복잡한 세부 사항은 숨기고, 중요한 특징과 기능만을 드러내는 것.**

- **코드에서 확인:** `Drink` 클래스가 `abstract`로 선언되어 객체를 직접 만들 수 없게 하며, `showInfo()` 메서드가 **추상 메서드**로 선언되어 모든 음료가 '정보를 보여주는' 기능을 **반드시 가져야 함**을 강제합니다.

**시험 출제 포인트:**

- **왜 사용하는가?** 👉 **구현의 강제성, 일관성 유지**
- 추상 클래스와 일반 클래스(또는 인터페이스)의 차이


Java

``` java
// Drink.java (추상 클래스)
package Model;

public abstract class Drink { // 'abstract' 키워드로 추상 클래스 선언
    protected String name;
    protected String brand;
    protected int volume;

    public Drink(String name, String brand, int volume) {
        this.name = name;
        this.brand = brand;
        this.volume = volume;
    }

    // 추상 메서드: 구현부가 없고, 자식 클래스가 반드시 구현해야 함
    public abstract void showInfo(); // 'abstract' 키워드로 추상 메서드 선언
                                    // "모든 음료는 정보를 보여줘야 해" (규칙 정의)

    public void drink() { // 일반 메서드도 가질 수 있음
        System.out.println(this.name + "을(를) 마십니다.");
    }
}
```

---

### 2. 👨‍👩‍👧‍👦 상속 (Inheritance)

**기존 클래스(부모)의 속성과 메서드를 새로운 클래스(자식)가 물려받아 재사용하고 확장하는 것.**

- **코드에서 확인:** `Cola` 클래스가 `extends Drink`를 사용하여 `Drink`의 속성(`name`, `brand`, `volume`)과 메서드(`drink()`, `getName()` 등)를 물려받고, 자신만의 특징을 추가합니다.

**시험 출제 포인트:**

- **장점은?** 👉 **코드 중복 감소, 유지보수 용이**
- 메서드 오버라이딩과의 관계


Java

``` java
// Cola.java (자식 클래스)
package Model;

public class Cola extends Drink { // 'extends Drink'로 Drink 클래스를 상속
    private String flavor;

    public Cola(String name, String brand, int volume, String flavor) {
        super(name, brand, volume); // 부모(Drink)의 생성자 호출, 부모의 속성을 초기화
        this.flavor = flavor;       // Cola 고유의 속성 초기화
    }

    @Override // 부모의 추상 메서드를 반드시 구현
    public void showInfo() {
        System.out.println("--- 콜라 정보 ---");
        System.out.println("이름: " + getName()); // 상속받은 getName() 메서드 사용
        System.out.println("브랜드: " + getBrand());
        System.out.println("용량: " + getVolume() + "ml");
        System.out.println("맛: " + this.flavor); // Cola 고유의 속성 접근
    }

    public void popBubble() { // Cola 고유의 메서드
        System.out.println(getName() + "에서 탄산 거품이 뽀글뽀글!");
    }
}
```

---

### 3. 🛡️ 캡슐화 (Encapsulation)

**데이터(속성)와 데이터를 다루는 메서드를 하나의 단위(클래스)로 묶고, 외부로부터의 직접 접근을 제한하여 데이터의 무결성을 보호하는 것.**

- **코드에서 확인:** `Drink` 클래스의 속성들이 `protected`로 선언되어 **직접 접근이 제한**되며, `public` 게터 메서드를 통해 **통제된 접근**을 제공합니다.
    
**시험 출제 포인트:**

- **왜 사용하는가?** 👉 **데이터 무결성 유지, 유지보수 용이**
- 접근 제한자(`public`, `protected`, `private`)의 범위와 차이



Java

``` java
// Drink.java (부분)
package Model;

public abstract class Drink {
    protected String name;    // 'protected'로 선언: 직접 접근 제한
    protected String brand;
    protected int volume;

    // ... 생성자 ...

    // 'public' 게터 메서드를 통해 'name' 속성 값에 접근을 허용
    public String getName() {
        return this.name; // 이 메서드를 통해서만 'name' 값을 외부에 제공
    }

    // 다른 속성들도 마찬가지로 게터 메서드를 가짐
    public String getBrand() { return this.brand; }
    public int getVolume() { return this.volume; }

    // ... 추상 메서드, 일반 메서드 ...
}
```

---

### 4. 🎭 다형성 (Polymorphism)

**하나의 객체가 여러 가지 형태를 가질 수 있거나, 하나의 메서드가 상황에 따라 다르게 동작할 수 있는 것.**

- **코드에서 확인:** `Drink` 타입의 배열에 `Cola`와 `Milk` 객체를 저장하고, 동일한 `showInfo()` 메서드를 호출해도 각 객체의 실제 타입에 따라 다른 결과가 출력됩니다.

**시험 출제 포인트:**

- **오버라이딩(Overriding) vs. 오버로딩(Overloading)**의 차이점
- **장점은?** 👉 **코드의 유연성, 확장성 향상**


Java

``` java
// Milk.java (자식 클래스, Cola와 다르게 showInfo()를 구현)
package Model;

public class Milk extends Drink {
    private double fatPercentage;

    public Milk(String name, String brand, int volume, double fatPercentage) {
        super(name, brand, volume);
        this.fatPercentage = fatPercentage;
    }

    @Override // 부모의 추상 메서드를 반드시 구현 (Cola와 다르게 구현)
    public void showInfo() {
        System.out.println("--- 우유 정보 ---");
        System.out.println("이름: " + getName());
        System.out.println("브랜드: " + getBrand());
        System.out.println("용량: " + getVolume() + "ml");
        System.out.println("지방 함량: " + this.fatPercentage + "%");
    }

    public void pour() { // Milk 고유의 메서드
        System.out.println(getName() + "을(를) 컵에 따릅니다.");
    }
}

// Main.java
package Model;

public class Main {
    public static void main(String[] args) {
        // Drink 타입의 배열에 다양한 종류의 음료 객체를 저장 (다형성)
        Drink[] drinks = new Drink[2];
        drinks[0] = new Cola("코카콜라 제로", "코카콜라", 350, "오리지널");
        drinks[1] = new Milk("저지방 우유", "매일유업", 1000, 1.8);

        System.out.println("--- 모든 음료 정보 출력 (다형성 활용) ---");
        for (Drink d : drinks) {
            d.showInfo(); // 동일한 'showInfo()' 호출
                          // 하지만, drinks[0]은 Cola의 showInfo(),
                          // drinks[1]은 Milk의 showInfo()가 실행됨 (다형성!)
            d.drink();    // 공통된 drink() 메서드 호출
            System.out.println("--------------------");
        }
    }
}
```

---

이러한 OOP 개념들을 이해하고 활용하면, 더욱 **체계적이고, 유지보수가 용이하며, 유연하게 확장 가능한** 소프트웨어를 개발할 수 있습니다.

---
# 오퍼레이션 (Operation)



## 🧠 핵심 요약 한 줄씩

| 개념  | 한 줄 요약                    |
| --- | ------------------------- |
| 추상화 | 중요한 것만 보여줘서 사용하기 쉽게 만듦    |
| 상속  | 부모의 기능을 자식이 물려받음          |
| 캡슐화 | 중요한 정보는 숨기고, 정해진 방법으로만 접근 |
| 다형성 | 같은 명령이 상황에 따라 다르게 동작      |
