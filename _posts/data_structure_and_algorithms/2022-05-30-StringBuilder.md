---
layout: post
title: Java's StringBuilder
subtitle: 
description:
category: Data structure & Algorithms
tags:
  - Data structure & Algorithms
  - Head First Java
---
# StringBuilder
Actually, stringbuilder can contain an array inside it as such:
```java
public String convert(String s, int numRows) {
    int index=0;
    StringBuilder[] st= new StringBuilder[numRows];
    for(int i =0;i<st.length;i++){
        st[i] = new StringBuilder();
    }
    while(index < s.length()){
        for(int i=0;i<numRows && index <s.length();i++){
            st[i].append(s.charAt(index++));
        }
        for(int i=numRows-2; i>0 && index<s.length();i--){
            st[i].append(s.charAt(index++));
        }
        
    }
    StringBuilder result = new StringBuilder();
    for(int i=0;i<st.length;i++){
        result.append(st[i]);
    }
    return result.toString();
}
```

## setCharAt()
sb.setCharAt(i,'*') where you can place something at a certain index
You can't put an empty literal like ('') so when you set it with 
certain pattern, use replaceAll() to put empty ("") like .replaceAll("\\*+","")
