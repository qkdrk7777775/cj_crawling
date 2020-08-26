# Koofs 자료 다운로드

## package example1

기간별, 지점별 통째로 자료 가지고 오는 코드 

```
import os, re
os.chdir(r'C:\Users\cjcho\Desktop\새 폴더 (2)\새 폴더 (2)')
download_dir=os.getcwd()
exe_path=r'c:\bin\chromedriver.exe'

Driver=Driver_open(download_dir=download_dir,exe_path=exe_path)
Driver.driver.get('http://www.khoa.go.kr/oceangrid/koofs/kor/oldobservation/obs_past_search.do')
Driver.main()
Driver.dayType('월별')
station_type_list=[re.compile('[가-힣|0-9]+').findall(i)[0] for i in Driver.get_text('select#observerType2.select').split('\n')[1:-1]]
station_type=station_type_list[0]
Driver.css_send_keys(css="select#observerType2.select",keys=station_type)
station_list=[re.compile('[가-힣][| 가-힣|0-9|\\(|\\)]+').findall(i)[0] for i in Driver.get_text('select#observer2.select').split('\n')[1:]]
station=station_list[0]

Driver.css_send_keys(css='select#Year.input1',keys=2019)
Driver.file_down(station_list=station_list[1:2],station_type=station_type)
Driver.driver.quit()
```

## package example2

최근 자료 가지고 오는 코드 

```
Driver=Driver_open(download_dir=download_dir,exe_path=exe_path)
Driver.driver.get('http://www.khoa.go.kr/oceangrid/koofs/kor/oldobservation/obs_past_search.do')
Driver.main()
Driver.dayType('월별',0)
Driver.dayRange()
Driver.dateList

station_type_list=[re.compile('[가-힣|0-9]+').findall(i)[0] for i in Driver.get_text('select#observerType.select').split('\n')[1:-1]]
station_type=station_type_list[0]
Driver.css_send_keys(css="select#observerType.select",keys=station_type)
station_list=[re.compile('[가-힣][| 가-힣|0-9|\\(|\\)]+').findall(i)[0] for i in Driver.get_text('select#observer.select').split('\n')[1:]]
station=station_list[0]
Driver.css_send_keys(css="select#observer.select",keys=station)

Driver.driver.execute_script('javascript:checkForm();')

Driver.file_down2(dateList=Driver.dateList,station=station,station_type=station_type)
Driver.driver.quit()

 
```
