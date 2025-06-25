# 성적산출 프로그램 (국어, 수학, 영어)

#학생 수 입력
while True:
    try:
        stds = int(input("학생 수를 입력하세요: "))
        if stds > 0:
            break
        else:
            print("1 이상의 정수를 입력하세요.")
    except:
        print("정수를 입력하세요.")

#학생번호, 각 과목 점수, 등수 리스트 생성
number = [0] * stds  
kor = [0] * stds              
math = [0] * stds           
eng = [0] * stds              
ranking_kor = [1] * stds        
ranking_math = [1] * stds      
ranking_eng = [1] * stds       

# 점수 입력 받기

# 점수 입력 받기
for i in range(stds):
    number[i] = i + 1  # 학생 번호 부여
    while True:
        try:
            kor_score = int(input(f"{number[i]}번 학생의 국어 점수를 입력하세요: "))
            if 0 <= kor_score <= 100:
                kor[i] = kor_score
                break
            else:
                print("0부터 100 사이의 정수를 입력하세요.")
        except:
            print("정수를 입력하세요.")

    while True:
        try:
            math_score = int(input(f"{number[i]}번 학생의 수학 점수를 입력하세요: "))
            if 0 <= math_score <= 100:
                math[i] = math_score
                break
            else:
                print("0부터 100 사이의 정수를 입력하세요.")
        except:
            print("정수를 입력하세요.")

    while True:
        try:
            eng_score = int(input(f"{number[i]}번 학생의 영어 점수를 입력하세요: "))
            if 0 <= eng_score <= 100:
                eng[i] = eng_score
                break
            else:
                print("0부터 100 사이의 정수를 입력하세요.")
        except:
            print("정수를 입력하세요.")

# 등수 산출 함수
def ranking(scores, ranks):
    sorted_scores = sorted(scores, reverse=True) #내림차순 정렬
    for i in range(stds):
        for j in range(stds):
            if scores[i] == sorted_scores[j]:
                ranks[i] = j + 1
                break

# 등급 산출 함수
def grade(score):
    if score >= 95:
        return "A+"
    elif score >= 90:
        return "A"
    elif score >= 85:
        return "B+"
    elif score >= 80:
        return "B"
    elif score >= 75:
        return "C+"
    elif score >= 70:
        return "C"
    else:
        return "F"

# 등수 계산
ranking(kor, ranking_kor)
ranking(math, ranking_math)
ranking(eng, ranking_eng)

# 번호순 출력
print("\n번호순 출력")
print("번호 국어 점수 등수 등급 | 수학 점수 등수 등급 | 영어 점수 등수 등급")
for i in range(stds):
    print(f"{number[i]:2d}번 {kor[i]:3d}점 {ranking_kor[i]:2d}등 {grade(kor[i]):2s} | "
          f"{math[i]:3d}점 {ranking_math[i]:2d}등 {grade(math[i]):2s} | "
          f"{eng[i]:3d}점 {ranking_eng[i]:2d}등 {grade(eng[i]):2s}")

# 성적순 출력 함수
def sort_ranking(subject_scores, subject_name):
    avg_score = sum(subject_scores) / stds

    # 번호, 점수, 등수 리스트
    num_list = number.copy()
    score_list = subject_scores.copy()
    rank_list = [1] * stds 

    # 등수 계산
    for i in range(stds):
        for j in range(stds):
            if score_list[j] > score_list[i]:
                rank_list[i] += 1

    # 점수 기준 정렬
    for i in range(stds - 1):
        for j in range(i + 1, stds):
            if score_list[j] > score_list[i]:
                # 점수 교환
                temp = score_list[i]
                score_list[i] = score_list[j]
                score_list[j] = temp

                # 번호 교환
                temp = num_list[i]
                num_list[i] = num_list[j]
                num_list[j] = temp

                # 등수 교환
                temp = rank_list[i]
                rank_list[i] = rank_list[j]
                rank_list[j] = temp

# 동점자있을 경우
    rank  = 1
    for i in range(stds):
        if i> 0 and score_list[i] == score_list[i-1]:
            rank_list[i] = rank_list[i-1]
        else:
            rank_list[i] = rank
        rank +=1

    # 성적순 출력
    print(f"\n{subject_name} 성적순 출력 (평균: {avg_score:.2f})")
    print("등수 점수 번호 등급")
    for i in range(stds):
        print(f"{rank_list[i]:2d}등 {score_list[i]:3d}점 {num_list[i]:2d}번 {grade(score_list[i]):2s}")


# 성적순 출력
sort_ranking(kor, "국어")
sort_ranking(math, "수학")
sort_ranking(eng, "영어")






# 성적산출 프로그램 (국어, 수학, 영어)

Python을 사용하여 학생들의 국어, 수학, 영어 점수를 입력받고, 각 과목별로 등수와 등급을 산출하는 기능을 제공하는 프로그램입니다. 
학생 수를 입력한 뒤 각 학생의 점수를 입력하면, 프로그램이 자동으로 번호순과 성적순으로 정리된 결과를 출력합니다. 
이를 통해 학생들의 상대적인 성적과 등수를 쉽게 확인할 수 있습니다.

## 프로그램 실행 순서

프로그램을 실행하면 먼저 사용자로부터 전체 학생 수를 입력받습니다. 
이때 잘못된 입력을 방지하기 위해 숫자가 아닌 값을 입력하거나 1 이하의 숫자를 입력하면 오류 메시지가 출력되고, 올바른 값이 입력될 때까지 반복 입력을 요구합니다.

사용자는 각 학생의 국어, 수학, 영어 점수를 차례로 입력합니다. 점수 입력 시에도 0점부터 100점 사이의 값만 입력할 수 있으며, 범위를 벗어나거나 잘못된 값을 입력하면 다시 입력을 요구합니다.

모든 점수 입력이 끝나면 프로그램은 등수를 계산합니다. 이중 for문을 통해 학생들의 점수를 서로 비교하고, 높은 점수를 가진 학생에게 더 높은 등수를 부여합니다. 동점자의 경우 공동 등수를 부여합니다. 
또한 점수에 따라 A+, A, B+, B, C+, C, F 등급을 부여합니다.

## 출력 내용

1. **번호순 출력**  
   번호순으로 각 학생의 국어, 수학, 영어 점수, 등수, 등급을 출력합니다.

2. **과목별 성적순 출력**  
   각 과목별로 점수를 내림차순으로 정렬한 뒤, 학생 번호, 점수, 등수, 등급을 출력합니다. 동점자의 경우 공동 등수를 적용합니다.

## 개발 특징

이 프로그램은 Python의 기본 문법(리스트, 반복문, 조건문, 함수)만을 이용하여 구현하였습니다. 등수 계산과 정렬 알고리즘을 스스로 구현하였습니다.
