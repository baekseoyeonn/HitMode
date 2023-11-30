# *HitMole*
---
---
# 1. game rule
> ## tutorial
>> ### tutorial에서는 랜덤으로 나타난 두더지가 사용자가 올바른 키를 입력할 떄까지 사라지지 않게 한다.
>> ### 튜토리얼을 멈추고 게임을 시작하고 싶으면 스페이스바를 누르도록 안내한다.

## main game
### round는 총 4단계로, 각각 라운드 마다 두더지가 0.2초씩 빨리 사라진다
### 1,2 round에서는 두더지가 나타나는 횟수의 80%만 맞추면 다음 라운드로 넘어갈 수 있고, 
### 4라운드는 히든 라운드로 3라운드에서 모두 다 맞추면 4라운드로 넘어갈 수 있다.
---
# 2. package
## What's in My Package
### HitMole에는 hitmole_pkg와 main.py로 구성되어있고, 패키지 안에는 __init__.py, hitmole_boards.py, 
### hitmole2.py로 구성되어있다.
### hitmole_boards는 보드판을 띄우는 역할로, 숫자나 문구를 보여줄 때 쓰고, 
### hitmole2는 게임을 진행하는 역할이다.

## how to start
### pynput와 numpy, os-sys를 pip install로 설치해야 하고, 
### python3 main.py를 터미널에 입력하여 실행한다.
### 처음에는 닉네임을 입력해야 하는데, 영어 소문자로 6글자 이내여야 한다.
### 튜토리얼을 진행한 후, space를 누르면 본게임이 시작되고 게임이 끝나면 전체 score와 랭킹이 적혀진다. 
