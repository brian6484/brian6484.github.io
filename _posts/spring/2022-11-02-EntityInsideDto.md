---
layout: post
title: How to handle entity inside DTO?
category: Spring
tags:
  - Spring
---

ManyToOne relationship between projects and member. I want to include
member entity inside ProjectDto to be passed to controller. 

How do I do this?

initial,wrong code:
```java
@Getter
@Setter
@NoArgsConstructor
public class ProjectDto {
    private String title;
    private String content;

    private Blob contentBig;
    private Long views;
    private LocalDateTime startDate;
    private LocalDateTime endDate;
    private String recruitmentStatus;
    private ProjectMember member;

    public Project toEntity(Project project) {
        return Project.builder()
                .title(title)
                .content(content)
                .contentBig(contentBig)
                .views(views)
                .startDate(startDate)
                .endDate(endDate)
                .recruitmentStatus(recruitmentStatus)
//                .member(new ProjectMember(project.getMember()))
                .build();

    }

    @Getter
    static class ProjectMember {
        private Long id;
        //needs to be replaced with Member's nickname, not username
        private String username;
        private MemberStatus memberStatus;

        public ProjectMember(Member member) {
            this.id = member.getId();
            this.username = member.getUsername();
            this.memberStatus = member.getMemberStatus();
        }
    }
}
```

correct code:
```java
@Getter
@Setter
@NoArgsConstructor
public class ProjectDto {
    private String title;
    private String content;
    private Blob contentBig;
    private Long views;
    private LocalDateTime startDate;
    private LocalDateTime endDate;
    private String recruitmentStatus;
    private ProjectMember member;

    @Builder
    public ProjectDto(Project project){
        this.title = project.getTitle();
        this.content = project.getContent();
        this.contentBig = project.getContentBig();
        this.views = project.getViews();
        this.startDate = project.getStartDate();
        this.endDate = project.getEndDate();
        this.recruitmentStatus = project.getRecruitmentStatus();
        this.member = new ProjectMember(project.getMember());
    }

    public Project toEntity(){
        return Project.builder()
                .title(title)
                .content(content)
                .contentBig(contentBig)
                .views(views)
                .startDate(startDate)
                .endDate(endDate)
                .recruitmentStatus(recruitmentStatus)
//                .member(project.getMember())
                .build();
    }

    @Getter
    static class ProjectMember{
        private Long id;
        //needs to be replaced with Member's nickname, not username
        private String username;
        private MemberStatus memberStatus;

        public ProjectMember(Member member){
            this.id= member.getId();
            this.username = member.getUsername();
            this.memberStatus = member.getMemberStatus();
        }
    }
}
```

Also, why does my constructor work but not @Builder?

To create object entity via constructor:
```java
Board entity = new Board("1번 게시글 제목", "1번 게시글 내용", "도뎡이", 0, 'N');
```

To create object via @Builder: which does not have to follow the order of 
parameters
```java
Board entity = Board.builder()
	.deleteYn('N')
	.hits(0)
	.writer("도뎡이")
	.content("1번 게시글 내용")
	.title("1번 게시글 제목")
	.build();
```

reference:
https://dodop-blog.tistory.com/237
