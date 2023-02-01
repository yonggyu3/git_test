## 깃 튜토리얼

소스코드

'''
# Q.1907년부터 2000년까지의 기간 동안 가장 일교차가 크게 나타났던 날짜는 언제이고, 그 날짜의 최고/최저 기온, 일교차는 몇 도였을까? 

import csv
import matplotlib.pyplot as plt
f = open('seoul.csv')
data = csv.reader(f)
next(data)
plt.rc('font', family = 'Malgun Gothic') # 맑은 고딕을 기본 글꼴로 설정 (제목 글자 깨짐 방지)
plt.rcParams['axes.unicode_minus'] = False # 마이너스 기호 깨짐 방지

result = [] # 일교차가 저장될 리스트
mx = 0 # 일교차가 가장 큰 값
day = 0 # 일교차가 가장 컸던 날짜
day_hot = 0 # 일교차가 가장 컸던 날의 최고기온
day_cool = 0 # 일교차가 가장 컸던 날의 최저기온
day_list = []


for row in data:
    date = row[0].split('-') # date에 날짜를 '-' 기준으로 구분해서 저장
    if row[-1] != '' and row[-2] != '': # 최고기온 데이터와 최저기온 데이터가 ''이 아닐 때
        if 1907 <= int(date[0]) <= 2000: # 1907년부터 2000년이면
            e = float(row[-1]) - float(row[-2]) # e에 일교차를 실수형으로 저장
            result.append(e) # result에 일교차 값 추가
            if e > mx: # 최근 찾은 일교차 값이 mx보다 크면
                mx = e # mx에 일교차 값 저장
                day = row[0] # 일교차가 가장 컸던 날을 저장
                day_hot = float(row[-1]) # 일교차가 가장 컸던 날의 최고기온
                day_cool = float(row[-2]) # 일교차가 가장 컸던 날의 최저기온
            
day_list.append(day) # 연/월/일로 자르기
day_y = day_list[0].split('-')[0]
day_m = day_list[0].split('-')[1]
day_d = day_list[0].split('-')[2]

plt.figure(dpi=300) # 해상도 설정
plt.title('1907~2000년도 일교차') # 제목 설정
plt.hist(result, bins=300, label = '일교차') # 히스토그램 그래프, bins 가로축 구간 개수
plt.xlabel('일교차 크기', size = 'small', loc = 'right') # x축 레이블 설정, size 텍스트 크기, loc 위치
plt.ylabel('일교차 양', size= 'small', rotation = 'horizontal' ,loc = 'top') # y축 레이블 설정, rotation 텍스트 회전각
plt.xticks([0,5,10,15,20], labels =['0℃','5℃','10℃','15℃','20℃']) # x축 눈금 설정, 눈금 레이블 설정
plt.legend() # 범례 표시
plt.show()
print('1907년부터 2000년까지의 날씨 데이터를 분석해본 결과 8℃~10℃ 정도의 일교차가 가장 많았고,')
print('일교차가 가장 크게 나타났던 날은', day_y+'년', day_m+'월', day_d+'일이다,')
print('이 날의 최고기온이', day_hot,'℃, ' '최저기온이', day_cool,'℃로 일교차는', mx, '℃로 나타났다.')


# Q.1907년부터 2000년까지의 기간 동안 가장 일교차가 크게 나타났던 날짜는 언제이고, 그 날짜의 최고/최저 기온, 일교차는 몇 도였을까? 

# 1907년부터 2000년까지의 날씨 데이터를 분석해본 결과 8℃~10℃ 정도의 일교차가 가장 많았고,
# 일교차가 가장 크게 나타났던 날은 1942년 04월 19일이다,
# 이 날의 최고기온이 24.3 ℃, 최저기온이 2.5 ℃로 일교차는 21.8 ℃로 나타났다,            

'''
