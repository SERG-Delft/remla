---
layout: default
title: 2021
hide_from_navbar: false
---

# Release Engineering for Machine Learning

ð£ **Announcement:** ð£ The link to the the Zoom meeting was shared via [Brightspace]. 

In this course, we will go on a journey that starts at continuous integration and then moves on to continuous delivery, continuous deployment, and continuous experimentation. We will discuss the theory and the current research on various related subjects like containerization, testing, or monitoring and will put the learned theory into practice. As a running example, we will build a pipeline for a machine learning application, which â compared to traditional release engineering â poses additional challenges, like data versioning or model deployment.

## Learning Objectives

After following this course, you will be able to:

- Apply standard techniques of release engineering;
- Apply version control techniques to machine learning artifacts, like data or models Design a deployment pipeline for a machine learning application;
- Implement quality control techniques in a machine learning pipeline;
- Analyze and improve existing deployment pipelines;
- Evaluate and document design decisions in deployment pipelines.

## Organization

**Course code**       | [CS4295]
**Instructors**       | [Sebastian Proksch], [LuÃ­s Cruz]
**Schedule**          |	Mondays, 15:45â17:45 <br/> Wednesdays, 13:45â15:45 <br/> Fridays, 13:45â15:45
**ECTS** 	          | 5.0
**Quarter**           | Q4
**Examination type**  | Software project (35%); Essay (60%); Presentation (5%)
**Target audience**   |	Students of the M.Sc. programme in Computer Science
**Requirements** 	  | - Intermediate understanding of OOP languages; <br/> - Practical experience with continuous integration; <br/> - Basic understanding of software testing principles; <br/> - Basic knowledge of machine learning techniques.


## Outline

**Please note:** The program below is tentative and is subject to change.

 Day   | Week| Type | Summary
------:| ---:|---|----------|
 19&nbsp;Apr| 1   | Lecture | Introduction: Organization and Course Schedule ([slides](./slides/01_intro_orga.pdf)); Tutorials and Final Project ([slides](./slides/01_intro_tutorials_project.pdf)).
 21 Apr| 1   | Lecture | Continuous {Integration, Delivery, Deployment} ([slides](./slides/02_deployment.pdf), [video](https://surfdrive.surf.nl/files/index.php/s/fjjlQLdFm1on2Pj)).
 23 Apr| 1   | Lab | Deployment in Practice: GitLab and Digital Ocean ([repositories](https://gitlab.com/remla-course/2021), [video](https://surfdrive.surf.nl/files/index.php/s/bd0goJcVS4uWG6x)).
 26 Apr| 2   | Lecture | Containers & Orchestration ([slides](./slides/03_container_orchestration.pdf), [video](https://surfdrive.surf.nl/files/index.php/s/rOah0G9GlaFf77B)).
 28 Apr| 2   | Lab | Containerization in Practice: Docker & Docker Compose ([repositories](https://gitlab.com/remla-course/2021), [video (part 1)](https://surfdrive.surf.nl/files/index.php/s/u9SXnkOF633NWnz), [video (part 2)](https://surfdrive.surf.nl/files/index.php/s/Gjw6k1WyJPsU8BE))
 30 Apr| 2   | Lecture | ML Testing. Recommended reading: *Whatâs your ML test score? A rubric for ML production systems.* [[1]](#1); also covering [[2]](#2) and [[3]](#3) ([slides](./slides/06_ml_testing.pdf), [video](https://surfdrive.surf.nl/files/index.php/s/THOVNbAsGQ5C10p)).
  3 May| 3   | Lecture | Part I â Guest Lecture: [Alex Serban] on ML Best Practices. Recommended reading: *Adoption and effects of software engineering best practices in machine learning* [[6]](#6). Part II â ML pipelines.   ([slides (part I)](./slides/07_ASerban_mleng_practices.pdf), [slides (part II)](./slides/07_ml_pipelines.pdf), [video](https://surfdrive.surf.nl/files/index.php/s/6zfuiyvdQdzQUxi))
  5 May| 3   | Free | *Public Holiday*
  7 May| 3   | Lab | [Tutorial â ML Configuration Management](tutorials/tutorial_03_ml_pipelines) ([video](https://surfdrive.surf.nl/files/index.php/s/4hLDs3wmRzl7xM9)).  
 10 May| 4   | Lecture | Continuous Experimentation. ([slides](./slides/08_continuous_experimentation.pdf), [video](https://surfdrive.surf.nl/files/index.php/s/8wHltRwP0jYsTQM))
 12 May| 4   | Lab | Kubernetes and Monitoring ([video](https://surfdrive.surf.nl/files/index.php/s/gTj3qtHz0dyhArU))
 14 May| 4   | Free | *Public Holiday*
 17 May| 5   | Self-Study | Literature Survey
 19 May| 5   | Lecture | How to write a paper ([slides](./slides/11_how_to_write_an_academic_paper.pdf)). Presentation tips ([slides](./slides/11_presentation_tips.pdf)).  ([video](https://surfdrive.surf.nl/files/index.php/s/tvkTY25IgUuZwxB))
 21 May| 5   | Feedback | Review Current Pipeline, Pipeline Extension Proposal
 28 May| 6   | Feedback | First Draft of ToC + Intro
 4 Jun | 7   | Feedback | Individual Steering Meetings
 11 Jun | 8   | Feedback | Sketch of Methodology or new pipeline
 TBD   | 9   | ?? | TBD
 21 Jun| 10  | Examination | Essay and Presentation
  ............  | | | 



## Recommended Reading

- <span id="1">[1]</span> - Eric Breck, Shanqing Cai, Eric Nielsen, Michael Salib, D. Sculley (2016). Whatâs your ML test score? A rubric for ML production systems. Reliable Machine Learning in the Wild - NIPS 2016 Workshop (2016) [Preprint](https://research.google/pubs/pub45742/).
- <span id="2">[2]</span> - Zhang, J. M., Harman, M., Ma, L., & Liu, Y. (2020). Machine learning testing: Survey, landscapes and horizons. IEEE Transactions on Software Engineering. [Preprint](https://arxiv.org/abs/1906.10742).
- <span id="3">[3]</span> - Sun, Z., Zhang, J. M., Harman, M., Papadakis, M., & Zhang, L. (2020, June). Automatic testing and improvement of machine translation. In Proceedings of the ACM/IEEE 42nd International Conference on Software Engineering (pp. 974-985). [Preprint](https://arxiv.org/abs/1910.02688).
- [4] - Haakman, M., Cruz, L., Huijgens, H., & van Deursen, A. (2020). AI Lifecycle Models Need To Be Revised. An Exploratory Study in Fintech. [Preprint](https://arxiv.org/abs/2010.02716).
- [5] - van Oort, B., Cruz, L., Aniche, M., & van Deursen, A. (2021). The Prevalence of Code Smells in Machine Learning projects. [Preprint](https://arxiv.org/abs/2103.04146).
- <span id="6">[6]</span> - Serban, A., van der Blom, K., Hoos, H., & Visser, J. (2020, October). Adoption and effects of software engineering best practices in machine learning. In Proceedings of the 14th ACM/IEEE International Symposium on Empirical Software Engineering and Measurement (ESEM). [Preprint](https://arxiv.org/abs/2007.14130).



[Sebastian Proksch]: https://proks.ch
[LuÃ­s Cruz]: https://luiscruz.github.io
[CS4295]: https://studiegids.tudelft.nl/a101_displayCourse.do?course_id=56383
[Alex Serban]: https://cs.ru.nl/~aserban/
[Brightspace]: https://brightspace.tudelft.nl/d2l/home/280442
