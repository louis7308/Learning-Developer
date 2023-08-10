# SMS 1차 배포 후 리팩토링을 작업을 진행 하였을 때

### 개요

SMS(학생 정보 통괄하는) 프로젝트를 진행 하면서 1차배포를 완료 하게 되었다. 하지만 1차 배포 후 그 다음 2차 스프린트를 진행 하여야 하는데 그 2차 스프린트를 진행하기 전에 남은 기간동안 "필터링" 코드를 리팩토링 해보는 것을 목표로 삼았다.



### 기능 요구사항

1. 게스트 & 학생 & 선생님 권한 일 때만 필터링 기능을 사용할 수 있다.
2. 게스트랑 학생이랑 선생님이 필터링을 열람 할 수 있는 갯수는 다르다.
3. 게스트가 필터링을 할 수 있는 부분은
   * 분야 필터
   *     세부스택 필터
4. 학생이 필터링을 할 수 있는 부분은
   * 학년 필터
   * 교실 필터
   * 학과 필터
   * 분야 필터
   * 학번 정렬 필터
   * 세부스택 필터
5. 선생님이 필터링을 할 수 있는 부분은
   * 학년 필터
   * 교실 필터
   * 학과 필터
   * 분야 필터
   * 희망 고용 형태
   * 인증제 점수 필터
   * 희망 연봉 필터
   * 학번 정렬 필터
   * 인증제 점수 정렬 필터
   * 희망 연봉 정렬 필터
   * 세부스택 필터
6. 항목 내용은 페이징이 되어 응답해야 한다.

### 리팩토링 하기 전

이러한 요구사항을 바탕으로 1차 스프린트에서는 이러한 Filter 코드를 작성하였다.

```kotlin
@Service
class FilterStudentServiceImpl(
    val studentPort: StudentPort
) : FilterStudentService {
    override fun filterStudents(
        students: List<Student.StudentWithUserInfo>,
        filters: FiltersRequestData,
        role: String
    ): List<Student.StudentWithUserInfo> =
        when (role) {
            "ROLE_TEACHER" -> this.filterStudentsForTeacher(students, filters)
            "ROLE_STUDENT" -> this.filterStudentsForStudent(students, filters)
            else -> this.filterStudentsForAnonymous(students, filters)
        }
```

함수에 인자값으로 넘어오는 role을 판단하여 그에 맞는 filter 로직을 실행하는 식으로 코드를 작성하였습니다.

```kotlin
private fun filterStudentsForTeacher(
        students: List<Student.StudentWithUserInfo>,
        filters: FiltersRequestData
    ): List<Student.StudentWithUserInfo> {
        var filteredStudents = students

        filters.majors?.let { majors -> // 전공
            filteredStudents = filteredStudents.filter { student ->
                student.major in majors
            }
        }

        filters.techStacks?.let { techStacks -> // techStack
            filteredStudents = filteredStudents.filter { student ->
                student.techStack.intersect(techStacks.toSet()).isNotEmpty()
            }
        }

        filters.grade?.let { grade ->
            filteredStudents = filteredStudents.filter { student ->
                student.stuNum.substring(0, 1).toInt() in grade
            }
        }

        filters.classNum?.let { classNum ->
            filteredStudents = filteredStudents.filter { student ->
                student.stuNum.substring(1, 2).toInt() in classNum
            }
        }

        filters.department?.let { departments ->
            filteredStudents = filteredStudents.filter { student ->
                student.department.name in departments
            }
        }

        filters.formOfEmployment?.let { formOfEmployments ->
            filteredStudents = filteredStudents.filter { student ->
                student.formOfEmployment.name in formOfEmployments
            }
        }

        if (filters.minGsmAuthenticationScore != null && filters.maxGsmAuthenticationScore != null)
            filteredStudents = filteredStudents.filter { student ->
                student.gsmAuthenticationScore >= filters.minGsmAuthenticationScore && student.gsmAuthenticationScore <= filters.maxGsmAuthenticationScore
            }

        if (filters.minSalary != null && filters.maxSalary != null) {
            filteredStudents = filteredStudents.filter { student ->
                student.salary >= filters.minSalary && student.salary <= filters.maxSalary
            }
        }
        filters.gsmAuthenticationScoreSort?.let { gsmScoreSort ->
            filteredStudents =
                if (gsmScoreSort == "ASCENDING") filteredStudents.sortedBy { it.gsmAuthenticationScore }
                else filteredStudents.sortedBy { it.gsmAuthenticationScore }.reversed()
        }

        filters.salarySort?.let { salarySort ->
            filteredStudents =
                if (salarySort == "ASCENDING") filteredStudents.sortedBy { it.salary }
                else filteredStudents.sortedBy { it.salary }.reversed()
        }

        filters.stuNumSort?.let { stuNumSort ->
            filteredStudents =
                if (stuNumSort == "ASCENDING") filteredStudents.sortedBy { it.stuNum }
                else filteredStudents.sortedBy { it.stuNum }.reversed()
        }

        return filteredStudents
    }
```

막상 처음 작성 할 때에는 알아 먹는데에는 이상이 없었지만 하루가 지난 후에 돌이켜 보니 코드가 너무 복잡하고 가독성이 떨어져 협업하는 친구에게 설명할 때에도 버벅임을 느끼고 다른 친구가 코드를 읽는 과정에서도 힘들다는 것을 느껴 코드를 리팩토링 해야겠다고 생각했다.



### 리팩토링 후
