# Appium-Python-Console

[TOC]



Appium-Python-Console은 Appium의 python-client로 Mobile Application을 테스트하기 위한 Test Script를 작성하는데 있어서 다양한 Appium driver methods를 테스트해 볼 수 있는 Console 프로그램 입니다.
Appium 설치 전 이라면 [Appium Setup Manual](https://github.com/embian-inc/Appium-Python-Console/blob/master/README-AppiumSetup.md)을 통해 먼저 Appium설치를 완료해 주시기 바랍니다.



## 1. Install Appium-Python-Console

###### 1) Git Clone 및 Appium-Python-Console폴더로 이동

```
$ git clone git@github.com:embian-inc/Appium-Python-Console.git

$ cd Appium-Python-Console
```

###### 2) Virtualenv(가상환경) Setting and Active

```
# 가상환경(venv) 생성
$ virtualenv venv

# 가상환경 활성화
# (venv)$				//가상환경 활성화 상태의 Prompt
$ . venv/bin/activate

# 비활성화
(venv)$ deactivate

```

###### 3) pip를 통한 requirements install

```
$ pip install -r requirements.txt
```

###### 4) PC 에 Mobile Device 연결

```
# 개발자 옵션 활성화
# 휴대전화 정보 > 빌드번호 연타
# 개발자옵션 > 안드로이드 디버깅 활성화(adb 인터페이스 사용하도록 설정)
# Mobile Device와 PC 연결 후 USB 디버깅 허용 Popup 확인

# 디바이스 연결상태 확인
$ adb devices
List of devices attached
	7387d0d19904	unauthorized    # not ok
    7387d0d19904	offline  		# not ok
	7387d0d19904	device			# ok
```

###### 5) Config 파일 Setting

DEVICE_NAME : adb devices 를 통해 출력된 Device 고유번호 (혹은 이름)
PLATFORM_VERSION : 연결된 Device의 Android 플랫폼 버전
DOC_SAVE_DIR : APC의 manual test mode에서 수집된 XML, HTML, Screen Shot 파일이 저장 될 Directory 경로
APK_FILE_DIR : APC (Appium-Python-Console) 실행 시 Device에서 실행될 APK 파일이 PC에 위치한 경로
APK_FILE_NAME : APK_FILE_DIR 경로에 위치해 있는 실행시킬 APK 파일의 이름

```
#-*- coding: utf-8 -*-

from os.path import expanduser

PATH = lambda p: os.path.abspath(
    os.path.join(os.path.dirname(__file__), p)
)

HOME = expanduser("~")

##################################################################
# PLEASE DO NOT CHANGE THIS SECTION. INSTEAD, USE SYMLYNK
#  use  your personal directory. use symlink!
##################################################################
DOC_SAVE_DIR = HOME + '/Documents/doc_file'
APK_FILE_DIR = HOME + '/Downloads/webview_apps/'
APPIUM_HOME = HOME + '/Documents/appium-1.6.3/'

##################################################################
# DO NOT CHANGE FOLLOWING LINES WHEN THERE ARE ONLY ONE DEVICE
# following two arguments are automatically overrided
# when there is only one device attached to your pc
##################################################################

# PLATFORM_NAME = 'Android'
# DEVICE_NAME = '7387d0d19904'
# PLATFORM_VERSION = '6.0'

PLATFORM_NAME = 'Android'
DEVICE_NAME = '7387d0d19904'
PLATFORM_VERSION = '6.0'

##################################################################
# Only Change following line (apk file name)
##################################################################
#APK_FILE_NAME = 'nl.apk'
#APK_FILE_NAME = 'line.apk'
#APK_FILE_NAME = 'musinsa.apk'

APK_FILE_NAME = 'findjob.apk'

##################################################################
# Appium Desired Capabilities Static Values
##################################################################

AUTO_GRANT_PERMISSIONS = True
ANDROID_INSTALL_TIMEOUT = 360000
AUTOMATION_NAME = 'uiautomator2'
NEW_COMMAND_TIMEOUT = 3600
APP_WAIT_ACTIVITY = '*'
NO_SIGN = True
```



###### 6) appium 실행 (new Terminal)
```
# appium 폴더로 이동
$ cd PATH/TO/appium-1.6.5

# appium 실행
$ node .
# 아래와 같은 메세지가 출력 되면 Appium 실행 완료
[Appium] Welcome to Appium v1.7.0-beta (REV cf24a80809309fb5467099e570cddd256cacbb28)
[Ap﻿pium] Appium REST http interface listener started on 0.0.0.0:4723
```

###### 7) Appium-Python-Console 실행

```
$ python main.py
```



## 2. APC(Appium-Python-Console) Methods

| Name |
|------|
| ```help()```|
| ```clear()```|
| ```exit()```|
| ```page()```|
| ```action_table()```|
| ```manual_test(mode='h')```|
| ```methods()```|
| ```methods(num)```|
| ```driver```|



* ```help() ``` : 도움말 | APC Methods 목록 출력
* ```clear()``` : 화면 Clear ( terminal의 clear 같은 기능 )
* ```exit()``` : APC 종료
* ```page()``` : App의 현재 페이지에서 Clickable = True 인 요소의 정보
  * arc(Appium-Ruby-Console)의 page와 같은 기능
  * 출력 정보 : class명, resource_id, content-desc, text, bounds
* ```action_table()``` : APC Special Method, 현재 페이지에서 Clickable한 Element의 List를 좀더 Smart하게 Detect 하여 Table형식으로 제공
  * Action Table과 함께 출력된 Action Group Table을 통해 Login, Sign Up, Checkbox, Search 등과 같이 현재 페이지에서 수행 되어야 될 일련의 동작을 추천
  * Hybrid Application
    * Native Element 와 Webview Element에서 액션 수행가능한 요소 출력

  * Native application
    *

* ```manual_test(mode='h')``` : APC Special Method, Action_table을 기반으로 한 Manual Test가 가능하도록 구현된 manual_test 모드로 전환
  * 본 모드로 전환 시 자동으로 현재 페이지의 action table을 Display
  * action table에서 수행하고자하는 Table row의 번호 (No.) 입력시 Touch | Input 액션 수행
  * h , help를 통해 manual test 모드에서만 사용 가능한 Command 확인 가능
  * manual test mode 종료 Command : q or Exit

* ```methods()``` : Appium Driver를 통해 사용할 수 있는 Methods 리스트 출력 (For Python-Client)
* ```methods(num)``` : methods()를 통해 출력된 Methods 리스트 중 특정 Method의 상세 정보 출력
  * num 변수는 methods()를 통해 출력된 Methods List의 번호
  * ex) methods(94)

* ```driver``` : Appium Driver, Appium Driver Methods 와 함께 조합 하여 사용
  * 사용법
    * driver.contexts
    * driver.find_element_by_id('RESOURCE_ID')
