---
layout: post
title: How to cleanly convert Dtos to Entities and vice versa
category: Spring
tags:
  - Spring
  
---
## Solution
Simple, use **builder patterns** and **inner static methods**.

For example in my toy project, let's say we are sharing bi-directional
@ManyToOne relationship between project and recruitment.
```java
@Entity
@Getter
@NoArgsConstructor(access = PROTECTED)
public class Project extends BaseTimeEntity {

    @Id
    @GeneratedValue(strategy = IDENTITY)
    @Column(name = "project_id")
    private Long id;

    @JoinColumn(name = "member_id")
    private Long member_id;

    @Column(nullable = false)
    private String title;

    @Lob
    private String content;

    private Long views;

    private LocalDateTime startDate, endDate;

    @OneToMany(mappedBy = "project_recr", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<Recruitment> recruitmentList = new ArrayList<>();

    @Email(message = "Please enter a valid email")
    private String email;

    @Column(nullable = true)
    private String url;

    @Builder
    public Project(Long id, Long member_id, String title, String content, Long views, LocalDateTime startDate,
                   LocalDateTime endDate, List<Recruitment> recruitmentList, String email, String url) {
        this.id = id;
        this.member_id = member_id;
        this.title = title;
        this.content = content;
        this.views = views;
        this.startDate = startDate;
        this.endDate = endDate;
        this.recruitmentList = recruitmentList;
        this.email = email;
        this.url = url;
    }

    public static Project toEntity(ProjectDto projectDto){
        return Project.builder()
                .title(projectDto.getTitle())
                .content(projectDto.getContent())
                .startDate(projectDto.getStartDate())
                .endDate(projectDto.getEndDate())
                .recruitmentList(Recruitment.toEntityList(projectDto.getRecruitmentDtoList()))
                .email(projectDto.getEmail())
                .url(projectDto.getUrl())
                .build();
    }

    public static ProjectDto from(Project project){
        return ProjectDto.builder()
                .title(project.getTitle())
                .content(project.getContent())
                .startDate(project.getStartDate())
                .endDate(project.getEndDate())
                .recruitmentDtoList(Recruitment.from(project.getRecruitmentList()))
                .email(project.getEmail())
                .url(project.getUrl())
                .build();
    }

    public void addRecruitment(Recruitment recruitment){
        if(this.recruitmentList!=null){
            this.recruitmentList.removeIf(r -> r == null || r.getProject_recr() == null);
        }
        recruitmentList.add(recruitment);
        recruitment.setProject_recr(this);
    }
}
```

We use **builder patterns** and **inner static methods** within
Project and ProjectDto class to map each field of dto to each field of entity and vice versa. 

Oh and for builder pattern of ProjectDto, it is fine to add @Builder
on class level. Don't really need to do on method level like Project.

```java
@Getter
@NoArgsConstructor(access = AccessLevel.PROTECTED)
@AllArgsConstructor(access = AccessLevel.PUBLIC)
@Schema(description = "DTO for posting projects")
@Builder
public class ProjectDto {

    @NotEmpty(message = "project title should not be empty!")
    @Length(min=5, max=30, message="project title should be 5 ~30 words long")
    @Pattern(regexp = "^[a-z0-9]*", message = "project tile should not contain any special characters")
    @Schema(description = "project title for posting", required = true, pattern = "^[a-z0-9]*", minLength = 5, maxLength = 30)
    private String title;

    @NotEmpty(message = "content of your project should not be empty!")
    @Schema(description = "project content for posting", required = true)
    private String content;

    @NotNull(message = "approximate start date and end date of your project plan should not be empty!")
    @Schema(description = "approximate start date and end date of your project plan")
    private LocalDateTime startDate, endDate;

    @Email(regexp = "[a-z0-9._%+-]+@[a-z0-9.-]+\\.[a-z]{2,3}",
            flags = Pattern.Flag.CASE_INSENSITIVE)
    private String email;

    private String url;

    private List<RecruitmentDto> recruitmentDtoList;
}
```

## confusing part
Well converting 1 single dto to 1 single entity is easy but
what if we want to convert a list of dtos like List<RecruitmentDto> list
into a list of entities like List<Recruitment> list? Well it is the
same logic

```java
@Entity
@Getter
@NoArgsConstructor(access = PROTECTED)
public class Recruitment extends BaseTimeEntity {

    @Id
    @Column(name = "recruitment_id")
    @GeneratedValue(strategy = IDENTITY)
    private Long id;

    @ManyToOne(fetch = LAZY)
    @JoinColumn(name = "project_id", foreignKey = @ForeignKey(name = "FK_recruitment_project"))
    private Project project_recr;

    private String recruitmentType;

    private int recruitmentCount;

    private String recruitmentStatus;

    @Builder
    public Recruitment(Long id, Project project_recr, String recruitmentType,
                       int recruitmentCount, String recruitmentStatus){
        this.id = id;
        this.project_recr = project_recr;
        this.recruitmentCount = recruitmentCount;
        this.recruitmentType = recruitmentType;
        this.recruitmentStatus = recruitmentStatus;
    }

    public static Recruitment toEntity(RecruitmentDto recruitmentDto){
        return Recruitment.builder()
                .recruitmentCount(recruitmentDto.getRecruitmentCount())
                .recruitmentStatus(recruitmentDto.getRecruitmentStatus())
                .recruitmentType(recruitmentDto.getRecruitmentType())
                .build();
    }

    public static List<Recruitment> toEntityList(List<RecruitmentDto> recruitmentDtoList){
        return recruitmentDtoList.stream()
                .map(recruitmentDto -> Recruitment.toEntity(recruitmentDto))
                .collect(Collectors.toList());
    }

    public static RecruitmentDto from(Recruitment recruitment){
        return RecruitmentDto.builder()
                .recruitmentType(recruitment.getRecruitmentType())
                .recruitmentCount(recruitment.getRecruitmentCount())
                .recruitmentStatus(recruitment.getRecruitmentStatus())
                .build();
    }

    public static List<RecruitmentDto> from(List<Recruitment> recruitmentList){
        return recruitmentList.stream()
                .map(recruitment -> Recruitment.from(recruitment))
                .collect(Collectors.toList());
    }

    public void setProject_recr(Project project_recr){
        this.project_recr = project_recr;
    }
}
```

Same logic first when converting 1 dto to 1 entity or vice versa.
We do toEntity() and from() like that. But we want to convert a list
of dtos to a list of entities and vice versa. To do that, we use
Java 8's stream() and map each dto with the Recruitment.toEntity() method
that we coded earlier and collect them in a list. Same for vice versa.

I haven't seen how do to this on google or in chatgpt so I struggled with
this a lot. Hope this helps :)
