---
layout: post
title: What is Lombok's Builder and why do we use it?
description: 
category: Spring
tags:
  - Spring

---

## Intro
To know why Lombok's @Builder annotation is developed, we first need
to know the Builder Pattern.

## Builder Pattern
It is one of the ways to create an object. When we need to
create an object and several fields exist (like age, gender, name, etc),
using a constructor needs to follow strict sequence of aligning
method parameter. To solve this, Builder Pattern resolves this.

```java
public class Test{
    private Integer number;
    private String str;
    
    public static class Builder{
        private Integer number;
        private String str;
        
        public Builder number(Integer number){
            this.number = number;
            return number;
        }
        
        public Builder str(String str){
            this.str = str;
            return this;
        }
        
        public Test build(){
            return new Test(number, str);
        }
    }
}

public class TestMain{
   @Test
   void test1(){
       Test test = Test.builder()
                       .number(1)
                       .str("test")
                       .build();
       System.out.println("output : " + test.getNumber() + " " + test.getStr());
       
       Test test2 = Test.builder()
         //different order from the declared (number,str)
         //but works
                       .str("test2")
                       .number(2)
                       .build();
       System.out.println("output : " + test2.getNumber() + " " + test2.getStr());
   }
}
```

We don't need to know the constructor's field order/sequence. We
just can create objects with fields easily with Builder pattern.

But creating Builder class for creating each object is repetitive
work. To solve this, use Lombok's @Builder!

## Lombok's Builder
```java
@Builder
@Getter
public class Test{
    private Integer number;
    private String str;
}

public class TestMain{
   @Test
   void test1(){
       Test test = Test.builder()
                       .number(1)
                       .str("test")
                       .build();
       System.out.println("output : " + test.getNumber() + " " + test.getStr());
   }
}
```

Works like magic!

## What if we don't put a value for a given field of object?
```java
@Builder
@Getter
public class Test{
    private Integer number;
    private String str;
}

public class TestMain{
   @Test
   void test1(){
       Test test1 = Test.builder()
                       .str("test")
         //no number value inputted
                       .build();
       System.out.println("test1 output : " + test1.getNumber() + " " + test1.getStr());
       Test test2 = Test.builder()
                       .number(1)
         //no string inputted
                       .build();
       System.out.println("test2 output : " + test2.getNumber() + " " + test2.getStr());
   }
}
```

Output we get is test1 output : 0 test , test2 output : 1 null.
It follows the Java convention that unspecified variables are given
0 or null or false.

## What if we want a default value in the field?
Let's first try manually creating a default value and see if
Lombok's Builder reads it.

```java
@Builder
@Getter
public class Test{
    private Integer number = 2;
    private String str = "default";
}

public class TestMain{
   @Test
   void test1(){
       Test test1 = Test.builder()
                       .str("test")
                       .build();
       System.out.println("test1 output : " + test1.getNumber() + " " + test1.getStr());
       Test test2 = Test.builder()
                       .number(1)
                       .build();
       System.out.println("test2 output : " + test2.getNumber() + " " + test2.getStr());
   }
}
```

Output we get is the same as before, test1 output : 0 test
test2 output : 1 null.

Why? I thought if we declare the field's value before it is used
by Lombok, Lombok will use it?

Actually, no. This is explained in the Lombok documentation:
>@Builder.Default
If a certain field/parameter is never set during a build session, then it always gets 0 / null / false. If you've put @Builder on a class (and not a method or constructor) you can instead specify the default directly on the field, and annotate the field with @Builder.Default:
@Builder.Default private final long created = System.currentTimeMillis();

As you see, we need annotation @Builder.Default to specify the 
default directly on the field like this:

```java
@Builder
@Getter
public class Test{
    @Builder.Default
    private Integer number = 2;
    
    @Builder.Default
    private String str = "default";
}

public class TestMain{
   @Test
   void test1(){
       Test test1 = Test.builder()
                       .str("test")
                       .build();
       System.out.println("test1 output : " + test1.getNumber() + " " + test1.getStr());
       Test test2 = Test.builder()
                       .number(1)
                       .build();
       System.out.println("test2 output : " + test2.getNumber() + " " + test2.getStr());
   }
}
```

Output we get is what we wanted! test1 output : 2 test ,
test2 output : 1 default


