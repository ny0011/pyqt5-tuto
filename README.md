# pyqt5-tuto

https://wikidocs.net/35479, https://wikidocs.net/book/2165 를 보고 PyQt5를 알아보자

## 0. 환경 설정

- python3
- pipenv 사용

## 1. PyQt5 + Qt Designer 관계

- Qt Designer는 레이아웃(UI) 편집기 : file.ui
- PyQt5에서는 이벤트 처리 : file.py
- Qt Designer에서 UI를 그림 -> PyQt5 코드에서 ui 불러오기 -> 프로그램 실행

```
#UI파일 연결
#단, UI파일은 Python 코드 파일과 같은 디렉토리에 위치해야한다.
form_class = uic.loadUiType("UI파일이름.ui")[0]

#화면을 띄우는데 사용되는 Class 선언
class WindowClass(QMainWindow, form_class) :
    def __init__(self) :
        super().__init__()
        self.setupUi(self)

if __name__ == "__main__" :
    #QApplication : 프로그램을 실행시켜주는 클래스
    app = QApplication(sys.argv)

    #WindowClass의 인스턴스 생성
    myWindow = WindowClass()

    #프로그램 화면을 보여주는 코드
    myWindow.show()

    #프로그램을 이벤트루프로 진입시키는(프로그램을 작동시키는) 코드
    app.exec_()
```

## 2. `PyQt5` 시그널과 함수

### 시그널

- 위젯 상태가 바뀌었을 때 행동을 정하는 코드
- 시그널은 반드시 `화면을 표시하는 class의 생성자` 부분에 입력해야 함

```
# 버튼 클릭 시그널 : javascript의 이벤트
self.btn1.clicked.connect(self.buttonClicked)

# buttonClicked() : javascript의 이벤트 핸들러
```

### 함수

- 위젯과 상관 없이 실행하는 코드
  - 보통 위젯의 값 설정, 값 가져오기, 속성 변화하기 등의 행동을 정함
- 공통 함수 몇 가지
  ```
  주의사항
  모든 함수의 앞에 self.ObjectName을 붙여야 함
  ex) self.btn1.move(1,2)
  이때 ObjectName이란, Qt Designer -> Property Editor에서 지정한 위젯의 ObjectName을 의미합니다.
  ```
  | Method                | 설명                                                       |
  | --------------------- | ---------------------------------------------------------- |
  | .move(x,y)            | 위젯의 위치를 지정. Parameter : 이동할 위치의 x,y좌표      |
  | .resize(width,height) | 위젯의 크기를 지정. Parameter : 위젯의 가로,세로 크기      |
  | .text()               | 위젯에 쓰여있는 글자를 가져옴                              |
  | .setText(String)      | 위젯에 새롭게 글자를 작성. Parameter : 위젯에 표시 할 글자 |
