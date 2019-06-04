# python2019
##201511132
##수학과 오상민

<pre><code>
'''
학과 : 수학과
학번 : 201511132
이름 : 오상민
'''
import pandas as pd
import matplotlib.pyplot as plt
ld = []

def switching(x):
    return {
        '확인':1,
        '필터링':2,
        '그룹':3,
        '종료':5.
    }.get(x,9) #default

def switching4(x):
    return {
        '1':'dead',
        '2':'hurt',
        '3':'heavy',
        '4':'light',
        '5':'report',
    }.get(x,9) #default

def switching2(x):
    return {
        '1':'01월',
        '2':'02월',
        '3':'03월',
        '4':'04월',
        '5':'05월',
        '6':'06월',
        '7':'07월',
        '8':'08월',
        '9':'09월',
        '10':'10월',
        '11':'11월',
        '12':'12월',
    }.get(x,9) #default

def switching5(x):
    return {
        '01월':1,
        '02월':2,
        '03월':3,
        '04월':4,
        '05월':5,
        '06월':6,
        '07월':7,
        '08월':8,
        '09월':9,
        '10월':10,
        '11월':11,
        '12월':12,
    }.get(x,9) #default

def switching3(x):
    return {
        '월별정보':1,
        '표':2,
        '그래프':3,
    }.get(x,9) #default

def column_sw(x):
    return {
        1:'dead',
        2:'hurt',
        3:'heavy',
        4:'light',
        5:'report',
    }.get(x,9) #default
def switch_col(x):
    return {
        1:'사망자',
        2:'부상자',
        3:'중상',
        4:'경상',
        5:'부상신고',
    }.get(x,9) #default

def groupby_draw(groupby_df):
    for name, group in groupby_df :
        if name == "월": break
        print(name + " : " + str(len(group))+" 항목")
        print(group)
        for x in range(1,6):
            if x == 9:
                print("Error1")
                break
            column = column_sw(x)
            g_d = group[[column]]
            g_d = g_d[column].astype(str).astype(int)
            g_sum = int(g_d.sum(axis = 0, skipna = True))
            k_col = switch_col(x)
            if k_col == 9 : 
                print("Error2")
                break

def ls_generator(groupby_df):
    total_ls = []
    ls_month = ['month']
    ls_death = ['death']
    ls_hurt = ['hurt']
    ls_heavy = ['heavy']
    ls_light = ['light']
    ls_report = ['report']
    ls_month_s = []
    ls_death_s = []
    ls_hurt_s = []
    ls_heavy_s = []
    ls_light_s = []
    ls_report_s = []
    for name, group in groupby_df :
        if name == "월": break
        ls_month_s.append(name)
        for x in range(1,6):
            if x == 9:
                print("Error1")
                break
            column = column_sw(x)
            g_d = group[[column]]
            g_d = g_d[column].astype(str).astype(int)
            g_sum = int(g_d.sum(axis = 0, skipna = True))
            k_col = switch_col(x)
            if k_col == 9 : 
                print("Error2")
                break
            if x == 1 : ls_death_s.append(g_sum)
            elif x == 2 : ls_hurt_s.append(g_sum)
            elif x == 3 : ls_heavy_s.append(g_sum)
            elif x == 4 : ls_light_s.append(g_sum)
    
    ls_month.append(ls_month_s)
    ls_death.append(ls_death_s)  
    ls_hurt.append(ls_hurt_s)
    ls_heavy.append(ls_heavy_s)
    ls_light.append(ls_light_s)

    total_ls.append(ls_month)
    total_ls.append(ls_death)
    total_ls.append(ls_hurt)
    total_ls.append(ls_heavy)
    total_ls.append(ls_light)
    return total_ls

def dict_line_df_generator(groupby_df):
    total_dict = {}
    ls_month_s = []
    ls_death_s = []
    ls_hurt_s = []
    ls_heavy_s = []
    ls_light_s = []
    ls_report_s = []
    for name, group in groupby_df :
        if name == "월": break
        ls_month_s.append(name)
        for x in range(1,6):
            if x == 9:
                print("Error1")
                break
            column = column_sw(x)
            g_d = group[[column]]
            g_d = g_d[column].astype(str).astype(int)
            g_sum = int(g_d.sum(axis = 0, skipna = True))
            k_col = switch_col(x)
            if k_col == 9 : 
                print("Error2")
                break
            if x == 1 : ls_death_s.append(g_sum)
            elif x == 2 : ls_hurt_s.append(g_sum)
            elif x == 3 : ls_heavy_s.append(g_sum)
            elif x == 4 : ls_light_s.append(g_sum)
    
    total_dict['month'] = ls_month_s
    total_dict['death'] = ls_death_s
    total_dict['hurt'] = ls_hurt_s
    total_dict['heavy']= ls_heavy_s
    total_dict['light'] = ls_light_s
    print(total_dict)

    return total_dict

print("2018년 교통사고유형별 분석 시작")

while True:
    print(" - 단일 자료 분석 사고 유형별 월별 분석 - ")
    r = 'w5.csv'
    df = pd.read_csv(r,encoding ='korean', header = None, names = ['typeif','type','month','occur','dead','hurt','heavy','light','report'])
    x1 = input('입력하시오.(1.확인, 2. 필터링, 3. 그룹, 5. 종료) ')
    y1 = switching(x1)
    #df[df.('월')='01월']
    print(y1)
    if y1 == 1 : print(df)
    elif y1 == 2:
        x2 = input("몇월? (ex 1 -> 01월 2 -> 02월, 12 -> 12월) ")
        y2 = switching2(x2)
        print(y2)
        if y2 == 9 : print("Wrong month")
        df_filtered = df[df.month == y2]
        print(df_filtered)
        x4 = input('뭐만 볼레? (1->사망자, 2->부상자, 3->중상자, 4->경상자, 5->보고) ')
        y4 = switching4(x4)
        print(y4)
        if y4 == 9 :  print("Wrong column")
        df_filtered = df_filtered[['typeif', 'type', y4]]
        print(df_filtered)
    #print(df_filtered)
    elif y1 == 3:
        print('- 월별 그룹별 합 -')
        groupby_month = df.groupby('month')
        x3 = input("입력하시오.(1.월별 모든 정보 2.표 3. 그래프")
        y3 = switching3(x3)
        if y3 == 1:
            groupby_draw(groupby_month)
        elif y3 == 2: 
            ls_sum_gb = ls_generator(groupby_month)
            df_sum = pd.DataFrame.from_items(ls_sum_gb)
            print(' - 월별 합계표 - ')
            print(df_sum)
        elif y3 == 3:
            dict_sum_gb_line = dict_line_df_generator(groupby_month)
            df_sum_gb = pd.DataFrame(dict_sum_gb_line, index = dict_sum_gb_line['month'])
            print(df_sum_gb)
            print('- 월별 교통사고 합계 그래프 -')
            df_sum_gb.plot(x="month", y=["death", "hurt",'heavy','light'])
            plt.show()
        else : print("wrong")
        #df_major_cnt = pd.DataFrame({'count' : groupby_month.size()}).reset_index()
        #print(df_major_cnt)
    elif y1 == 5 : break
    else : print("wrong")

#pd.DataFrame.from_items(r)
</code></pre>
