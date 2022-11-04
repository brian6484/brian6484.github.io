---
layout: post
title: JPA without entity relationships
description: 
category: JPA
tags:
  - JPA
---
  
## Intro 
JPA without 연관관계 (entity relationships) like @ManyToOne ultimately
cannot product object-orientated code. This is because we search up 
entities and update them on their primary keys.

## Without 연관관계
Let's look at this example

```java
@Entity
public class Patient{
    @Id @GeneratedValue
    @Column(name="patient_id")
    private Long id;
    
    private String name;
    
    //remember JPA (latest versions) automatically changes
    //java's camelCase name to preferred DB naming convention
    //hospitalId -> hospital_id
    private Long hospitalId;
}

@Entity
public class Hospital{
    @Id @GeneratedValue
    private Long id;
    
    private String name;
}
```

Without 연관관계, we need to use FK of entities.
```java
Hospital hospital = new Hospital();
hospital.setName("Hospital Hola");
em.persist(hospital);

Patient patient = new Patient();
patient.setName("Wally");
patient.setHospitalId(hospital.getId());
em.persist(patient);
```
  
This is not very object-oriented because we optimally want to 
somehow get patient.getHosptial() like getting objects, not FKs.


