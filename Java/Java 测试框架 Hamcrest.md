# Java 测试框架 Hamcrest

用来做测试结果匹配的，有许多定义好的方法，语义化好理解；API丰富；支持自定义匹配（Matcher）。

[中文blog][1] vs [官网-英文][2] (英文看的累...) vs [教程-baeldung实际例子][3]


TestUnit: HamcrestTest.java

```java
public class HamcrestTest {

    @Test
    public void testEquals() {
        Biscuit theBiscuit = new Biscuit("Ginger");
        Biscuit myBiscuit = new Biscuit("Ginger");

        assertThat(theBiscuit, equalTo(myBiscuit));
        assertThat("chocolate chips", theBiscuit.getChocolateChipCount(), equalTo(10));
        assertThat("hazelnuts", theBiscuit.getHazelnutCount(), equalTo(3));
    }

    // Writing custom matchers
    @Test
    public void testSquareRootOfMinusOneIsNotANumber() {
        System.out.println(Math.sqrt(-1));
        assertThat(Math.sqrt(-1), is(IsNotANumber.notANumber()));
    }

    @Data
    class Biscuit {

        public String name;
        public int chocolateChipCount;
        public int hazelnutCount;

        public Biscuit(String name) {
            this.name = name;
            this.chocolateChipCount = 10;
            this.hazelnutCount = 3;
        }

    }

}

```

Custom Matcher: IsNotANumber.java

```java
package xxx.xxx.xxx;

import org.hamcrest.Description;
import org.hamcrest.Matcher;
import org.hamcrest.TypeSafeMatcher;

public class IsNotANumber extends TypeSafeMatcher<Double> {

    @Override
    public boolean matchesSafely(Double number) {
        return number.isNaN();
    }

    public void describeTo(Description description) {
        description.appendText("not a number");
    }

    public static Matcher notANumber() {
        return new IsNotANumber();
    }

}
```


[1]: https://www.jianshu.com/p/848fd619238f
[2]: http://hamcrest.org/JavaHamcrest/tutorial
[3]: https://www.baeldung.com/java-junit-hamcrest-guide