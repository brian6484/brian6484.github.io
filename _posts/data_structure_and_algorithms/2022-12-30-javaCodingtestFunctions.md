---
layout: post
title: Useful Java data type functions for coding test
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
---

## Library
```java
import java.util.*;
import java.io.*;
```

## Declare variables
```java
int len = hola.length;
String[] arr = new String[len];

int[] arr2 = {1,2,3};
```

## Arrays
```java
int arr[] = {10, 8, 11, 2, 3, 0};

// 1. ascending {0, 2, 3, 8, 10, 11}
Arrays.sort(arr1);

// 2. descending {11, 10, 8, 3, 2, 0}
Arrays.sort(arr1, Collections.reverseOrder());

// 3. 일부만 정렬 {2, 8, 11, 10, 3, 0} (index 0~4만 정렬)
Arrays.sort(arr1, 0, 4);

// 4. if order is ascending, 
// can use binary search로 특정 값's index을 찾을 수 있다.
Arrays.binarySearch(arr1, 2);

// 5. 배열을 ArrayList 변환할 떼!
List list = Arrays.asList(arr1);

// 6. 배열의 특정 범위 자르기 with index
// inclusive start index, exclusive end index  
int tmp[] = Arrays.copyOfRange(arr1, 0, 3);
```

## length, length(), size()
* length - for array (arr.length())
* length() - for String related object (str.length())
* size() - for Collections object (list.size())

```java
// 1. length
int[] arr = new arr[3];
System.out.println(arr.length);

// 2. length()
String str = "java";
System.out.println(str.length());

// 3. size()
ArrayList<Integer> list = new ArrayList<>();
System.out.println(list.size());
```


## String
```java
String str = "hello world";

// 1. 자르기
//.split()  문자열을 array로 만들고 싶을 때
//.split()  splits string with the regex parameter passed
// and saves this split string parts into an array  
String[] arr = str.split(" ");
for(String a:arr){
    System.out.println(a);    
}

String str = "12345";
String[] Arr = str.split("");

str.substring(0, 5);

for(int i = 0; i < str.length(); i++) str.charAt(i);

// 대소문자 변경
str = str.toUpperCase();		// HELLO WORLD
str = str.toLowerCase();		// hello world

// strings are immutable
// .substring() 이용해서 새로운 변수로 선언해야함
String name="starfucks";
String newname=name.substring(0,4)+'b'+name.substring(5);	
// starbucks
```

## HashMap
```java
// 1. 선언
HashMap<String, Integer> hm = new HashMap<>();

// 2. key-value 넣기
//.put(key,value)  
hm.put("java", 0);

// 3. 키로 값 가져오기
//.get(key) -> value   
hm.get("java");

// 4. containsKey()로 존재유무 확인
if (!hm.containsKey("java")) hm.put("java", 1);

// 5. 특정 키가 없으면 값 설정, 있으면 기존 값 가져오는 함수
hm.put("java", hm.getOrDefault("java", 0)+1);	

// 6. keySet() 함수로 맵 순회
for(String key : hm.KeySet()) {				
	hm.get(key);
}

// .values() to get HashMap's values
for(Integer val: map.values()){
    
}
```

## ArrayList
```java
// 1. 선언
ArrayList<String> list = new ArrayList<>();

// 2. 삽입
list.add("java");			
// {"java"}
list.add(0, "ryu");			
// {"ryu", "java"} (0번째 인덱스에 삽입)

// 3. 수정
list.set(1, "c++");			
// {"ryu", "c++"}

// 4. 삭제
list.remove(1);				
// {"ryu"}

// 5. 값 존재 유무 확인
list.contains("java");		
// false
list.indexOf("ryu");		
// 0 if no such value found, 존재하면 인덱스 리턴

// 6. iterator 사용
Iterator it = list.iterator();

// 6-1. 인덱스 오름차순 순회
while (it.hasNext()) {
	...
}

// 6-2. 인덱스 내림차순 순회
while (it.hasPrevious()) {
	...
}

// 7. 중복없이 값을 넣고 싶을 때
if (list.indexOf(value) < 0) {	// 없으면 -1을 리턴하기 때문에
	list.put(value);
}

// 8. 리스트 값 하나씩 가져올 때 (int 일 경우)
for(int i = 0; i < list.size(); i++) {
	list.get(i).intValue();
}
```

## Queue
```java
// 1. 선언
Queue<Integer> q = new LinkedList<>();		
// linked list로 선언해야함

// 2. 삽입
  q.add(10);			
  // {10}
  q.offer(2);			
  // {10, 2}

// 3. 프론트값 반환
  q.peek();			
  // 10

// 4. 삭제
  q.remove();
  q.poll();

// 5. 초기화
  q.clear();

// 6. 비었는지
  q.isEmpty();

// 7. pair 같은 경우는 그냥 구현해서 사용
static class Node{
  int y;
  int x;
  int dist;

  Node(int y,int x,int dist){
    this.y=y;
    this.x=x;
    this.dist=dist;
  }
}

Queue<Node> queue=new LinkedList<>();
queue.add(new Node(1,2,3));
Node node= queue.poll();
```

## PriorityQueue
```java
// 1. 선언
PriorityQueue<Integer> pq = PriorityQueue<Integer>();	// 최소힙
  
//descending / max heap
PriorityQeueu<Integer> pq=PriorityQueue<Integer>(Collections.reverseOrder());
PriorityQeueu<Integer> pq = PriorityQueue<>((a,b)->b-a);
PriorityQeueu<Integer> pq = PriorityQueue<>((a,b)->b-a);
  
// 2. 삽입
pq.add(3);

// 3. 삭제
pq.remove();

// 4. root 값 추출
pq.peek();

// 5. pair 사용 시 
import java.io.IOException;
import java.util.PriorityQueue;

public class PQ {

    static class Node{
        int y;
        int x;

        Node(int y,int x){
            this.y=y;
            this.x=x;
        }
		
        // 비교 함수 만들어야함!!
        public int compareTo(Node p) {
            if(this.y < p.x) {
                return -1; // 오름차순
            }
            else if(this.y == p.y) {
                if(this.x < p.x) {
                    return -1;
                }
            }
            return 1;
        }
    }

    public static void main(String[] args) throws IOException{

        PriorityQueue<Node> pq1=new PriorityQueue<>(Node::compareTo);
        pq1.add(new Node(1,2));
        pq1.add(new Node(1,1));
        pq1.add(new Node(2,3));
        pq1.add(new Node(2,1));

        while(!pq1.isEmpty()){
            Node node=pq1.peek();
            System.out.println(node.y+" "+node.x);
            pq1.remove();
        }
    }
}
```

## Math library
```java
// 1. 최대 최소
Math.max(10, 2);
Math.min(10, 2);

// 2. 절대값
Math.abs();

// 3. 올림 내림 반올림
//.ceil() rounds UP like up to the ceiling 
Math.ceil(-3.2) =-3;
Math.ceil(125.9)=126.0
Math.ceil(0.4873)=1.0

//.floor() rounds DOWN to the floor  
Math.floor(-3.2);		// -4
Math.round(-3.26);		// -3	첫째자리에서 반올림

// 3-1. 소수 둘째, 셋째 자리에서 반올림 하고 싶다면
double a = 1.23456;
String b = String.format("%.1f", a);	// .1f는 둘째자리에서 반올림

// 4. 제곱 제곱근
Math.pow(2, 2);		// 2^2 = 4
Math.sqrt(4);		// 2
```
