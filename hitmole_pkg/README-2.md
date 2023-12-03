# 전체 게임 진행

*   `tutorial` → `1라운드` → `점수출력` → `판별` → `2라운드` → `점수` → `3라운드` → `점수` → `랭킹출력`

# 보드판 코드 설명

## 1.  HITMOLE

```
hitmole_board(): 
          os.system("clear")
          print(HIT_MOLE)
          time.sleep(1.5)
          os.system("clear") 
          print("\n"*20)
          time.sleep(0.5) 
```
       
터미널 코드 전적 지운 후 저장된 문자열인 게임명 출력, 읽을 수 있게 1.5초 유지  
다음 화면으로 넘어가기 전 공백을 위한 print를 0.5초 유지     

## 2. 튜토리얼 시작

```
tutorial_board(): 
          os.system("clear")
          print(TUTORIAL)
          ...
```

프린트 하는 문자만 다를 뿐 나머지 코드는 _`hitmole_board`_ 와 동일

## 3. 게임 시작 전 3초 카운트다운과 함께 시작을 알리는 함수
```
start_board():
        os.system("clear") 
        for i in range(3): 
                print('\n'*8,end='') 
                index = (3-i)*5 
                for l in range(5):  
                        print(' '*26, NUMS[l][index:index+5]) 
                ...
        print(START)   
        time.sleep(1.0)
```
3,2,1 카운트 다운을 위한 반복 루프 제작, 카운트 값에 따라 숫자를 가져오기 위한 index 계산  
-> `NUMS` 리스트에서 해당 인덱스 범위의 숫자를 출력하기 위해 반복 루프(5번인 이유는 리스트에서 숫자 하나가 5열로 구성)    
->  `...`부분은 _`time.sleep`, `os.system`, `print`_ 로 위에서 다룬 함수이므로 생략, _`print`_ 는 줄바꿈을 통한 화면 정리를 위함

## 4. 랜덤으로 튀어나온 두더지를 출력하는 함수

```
pop = [0 0 0 0 0 0 0 0 0]

q w e   0 1 2  
a s d   3 4 5  
z x c   6 7 8
```
랜덤으로 두더지가 들어갈 인덱스만 1인 상태로 변수 pop을 넘겨받을 것.  
pop에서의 인덱스와 매칭되는 키보드값은 위와 같음.

```
    def print_board(pop):  
              os.system("clear")
              for i in range(3): 
                  for r in range(len(HOLE)): 
                      for ii in range(3): 
                index = 3*i + ii 
                if pop[index] == 1: 
                    print(MOLE[r], end='') 
                else: 
                    print(HOLE[r], end='') 
            print()
```

세로로 3개의 행을 나타내기 위한 반복 루프-> HOLE의 길이만큼 반복하는 루프-> 가로로 3개의 열을 나타내는 루프  

현재의 행과 열을 기반으로 pop 리스트에서 가져올 인덱스를 계산  
-> 인덱스가 1인 경우 (즉, 해당 위치에 두더지가 나타난 경우) : __두더지__ 출력  
-> 인덱스가 0인 경우 (즉, 해당 위치에 두더지가 나타나지 않은 경우) : __구멍__ 출력  

          
## 5. 두더지를 잡은 경우 해당 것만 찌그러진 두더지, 나머지는 구멍 출력하는 함수

```
def hit_board(pop):  
          ...(위의 print_board코드와 동일)
                if pop[index] == 1: 
                    print(HIT[r], end='') 
                else:
                    print(HOLE[r], end='') 
            print()
```
사용자가 두더지를 잡은 경우에
랜덤으로 숫자를 뽑아둔 pop_up을 받아 해당 인덱스만 찌그러진 두더지를 출력하고
나머지는 구멍을 출력하도록 한다.

-> 인덱스가 1인 경우 (즉, 해당 위치에 두더지가 나타난 경우) : __찌그러진 두더지__ 출력  
-> 인덱스가 0인 경우 (즉, 해당 위치에 두더지가 나타나지 않은 경우) : __구멍__ 출력  


## 6. SCORE 글자판과 최종 점수를 출력하는 함수
```
    def score_board(points):
              os.system("clear")
              points = str(points) 
              print('\n'*8) 
              for i in range(5): 
                  print(SCORE[i],end='') 
                  for n in range(len(points)): 
                      index = int(points[n])*5 
                      print(NUMS[i][index:index+5],end='') 
                  ...
```
__점수를 나타내는 각 숫자의 행을 나타내는 반복 루프__  
-> points의 길이만큼 반복하는 루프 시작(이는 각 숫자를 나타냄)  
-> 현재 숫자에 대한 인덱스를 계산 : 문자열 points에서 n번째 자리의 숫자를 가져오고, 가져온 숫자를 정수로 변환  
(숫자를 5배로 곱하는데, 이렇게 하는 이유는 각 숫자가 NUMS 리스트에서 5행으로 이루어져 있기 때문)   


## 7. 사용자가 일정 점수를 넘겨 다음 라운드로 진입할 경우 ROUND 출력하는 함수
```
    def round_board(round):
              os.system("clear")
              print('\n'*8)
              for i in range(5): 
                  print(ROUND[i],end='') 
                  index = round*5 
                  print(NUMS[i][index:index+5],end='') 
                  print()
              print('\n'*10,end='')
```
round는 현재 게임 라운드를 나타내는 변수  
NUMS 리스트에 있는 각 숫자는 5개의 행으로 이루어져 있으며,   
따라서 현재 라운드에 해당하는 인덱스를 구하기 위해서는 round에 5를 곱해야 함.  

## 8. 게임이 끝날 시 GAME OVER를 세 번 깜박이는 함수
```
    def over_board():
    for _ in range(3): 
        os.system("clear") 
        print(OVER) 
        ...
```
hitmole_board 코드와 유사, GAME OVER 텍스트를 세 번 깜박이게 하기 위한 함수

---

# hitmole2.py 함수의 설명.

## 1. init 함수
```
    def __init__(self):
        self.points = 0
        self.click = None
        self.cnt_round = 1
```
점수 카운팅, 사용자 입력키를 판별, 게임 라운드 진행을 저장하는 속성


## 2. 랜덤으로 두더지가 나올 구멍 뽑는 함수
- 0부터 8까지의 숫자 중 하나를 뽑아 그 수만 1이고 나머지는 0인 일차원 숫자 행렬 반환 
```
    def pop_up(self,mole=None): 
        self.holes = np.zeros(9) 
        self.holes[mole] = 1 
        return self.holes 
``` 

- mole 매개변수는 두더지가 나올 구멍의 인덱스를 나타냄  
  이 매개변수는 기본값으로 None을 가지고 있으며, 호출 시 구멍의 인덱스를 제공하지 않으면 None으로 설정
  
- holes라는 클래스 속성을 만들어 0으로 초기화된 길이가 9인 numpy 배열로 설정하며, 이 배열은 두더지가 나올 구멍을 나타내는데 사용
  mole이 None이 아닌 경우: 해당 인덱스의 원소를 1로 설정하며, 이것이 두더지가 나올 구멍이 된다  
  mole이 None인 경우: 모든 원소가 0인 상태로 유지
  
- 최종적으로 업데이트된 holes 배열을 반환-> 이 배열은 두더지가 나온 구멍은 1로, 그 외의 구멍은 0으로 표시된 배열.


## 3. 사용자로 부터 키보드 값을 입력받는 함수
``` 
    def wait_keyboard(self, timeout=None):
        def on_press(key): 
            try:  
                if key == kb.Key.space: 
                                        
                    self.click = "space"
                    return False
                if key.char == 'q': 
                    self.click = 0
                    return False
                elif key.char == 'w':
                    self.click = 1
                    return False
                ...(반복)
                else:
                    self.click = "Wrong Key"
                    return False
            except:
                self.click = "Wrong Key"
                return False

        with kb.Listener(on_press=on_press) as listener:
            self.click = None 
            if timeout: 
                timer = Timer(timeout, listener.stop)
                timer.start()
            listener.join() 
        return self.click 
```
- on_press(key) 함수는 키가 눌렸을 때 실행되며, 눌린 키에 따라 self.click 변수에 특정 값이 할당됨  
- key.char는 입력된 키보드값이 문자열이 아니면 오류가 나기에 try except 사용  
  키의 문자 값을 얻어오기 위해 key.char를 사용  
  그러나 만약 키가 문자가 아니라면 key.char를 사용할 수 없기 때문에 예외 처리를 함  
- self.click에 다양한 값을 할당 (예를 들어, 'q' 키가 눌리면 self.click에 0을 할당하고,'w' 키가 눌리면 1을 할당)    
  
- keyboard.Listener를 사용하여 키보드 입력을 감지하는 객체를 생성  
  키보드 입력을 기다리기 전에 self.click을 초기화->  
  타임아웃이 설정되어 있다면 입력을 기다리는 동안에 타이머를 시작
    
  타이머가 만료되면 listener.stop을 호출하여 키보드 리스너를 종료  
  키보드 입력을 계속해서 기다리는데 사용자가 특정 키를 누를 때까지 기다리며, 타임아웃이 설정된 경우 타이머가 만료되면 종료  
  

## 4. 조작키를 알려주고 연습하는 튜토리얼 함수
-랜덤으로 나타난 두더지가 사용자가 올바른 키를 입력할 때까지 사라지지 않고, 튜토리얼을 멈추고 게임을 시작하고 싶으면 스페이스바를 누르도록 안내
```
      def tutorial(self):
        boards.tutorial_board() 
        while True:
            start_game = False
            mole = rd.choice(range(9)) 
            pop = self.pop_up(mole) 
            boards.print_board(pop) 
            print('''두더지 위치에 해당하는 키를 눌러 두더지를 잡으세요!    space를 누르면 게임시작
                  ...위에서 언급한 qweasdzxc 키들...
                  ''')
            while True:
                hit = False
                if self.click == "space": 
                    start_game = True
                    break
                try:  
                    key = self.wait_keyboard() 
                    if self.holes[key] == 1: 
                        boards.hit_board(pop) 
                        time.sleep(0.25) 
                        hit = True 
                    else:
                        print(f'잘못된 키를 입력했습니다. {self.click}')
                except:
                    if self.click != "space":
                        print(f'잘못된 키를 입력했습니다. {self.click}')
                if hit: 
                    break
            if start_game: 
                break
```
- boards 객체의 tutorial_board 메서드를 호출하여 튜토리얼 보드를 출력
  : 게임 화면을 보여주는 부분으로, 게임의 튜토리얼을 시각적으로 보여줌  
- 0부터 8까지의 숫자 중에서 랜덤으로 하나를 선택하여 mole 변수에 저장
  : 나타난 두더지의 위치를 나타냄  
- pop_up 메서드를 호출하여 두더지가 나타난 구멍을 나타내는 배열을 얻음  
  : 현재 보드 출력하여 pop 배열은 어떤 구멍에 두더지가 나타났는지 나타낼 수 있음    

- 사용자가 스페이스바를 누르면, 게임을 시작하는 신호로 start_game을 True로 설정하고 두 번째 무한 루프를 탈출  
  self.click = "wrong key"인 경우가 있기 때문에 리스트 인덱싱 오류를 피해야 함  
- 입력한 키의 구멍에 두더지가 있다면(self.holes[key]가 1이라면)  
  -> boards.hit_board(pop)을 호출하여 두더지가 맞았다는 화면 출력, hit 변수를 True로 설정  

- 만약 두더지를 맞췄다면 내부 무한 루프를 탈출하여 다음 두더지의 나타남을 처리   
  만약 start_game이 True라면 외부 무한 루프를 탈출하여 게임을 시작  



## 5. 한 라운드 안에서의 플레이 함수.

- 사용자가 두더지가 사라지기 전에 해당 키를 누르면, 두더지가 찌그러지는 효과와 함께 사용자 점수를 +10을 주고,
지정된 9개의 키 외의 키를 누르면 기회를 조금 더 줌.

```
        def play_round(self):
        for _ in range(10): 
            mole = rd.choice(range(9)) 
            pop = self.pop_up(mole) 
            boards.print_board(pop) 
            time_by_level = 1.0 - (0.2 * self.cnt_round) 
            key = self.wait_keyboard(time_by_level) 
            try:  
                if self.holes[key] == 1: 
                    self.points += 10 
                    boards.hit_board(pop) 
                    time.sleep(0.15)
                else:
                    time.sleep(0.15)
            except: # try 에서 예외가 발생하면
                key = self.wait_keyboard(0.35-(0.05*self.cnt_round)) 
                try:
                    ...위의 try와 동일 코드
                except:
                    pass
            pop = np.zeros(9) 
            boards.print_board(pop) 
            time.sleep(0.1)
```
각 라운드에서는 10번의 시도가 주어지고, 두더지가 랜덤으로 10번 나타남.  
레벨에 따라 두더지가 나타나는 시간을 결정: 레벨이 높아질수록 두더지가 나타나는 시간이 짧아짐  

wait_keyboard 메서드를 호출하여 사용자로부터 키보드 입력을 받음  
-> 사용자가 입력한 키에 해당하는 구멍에 두더지가 있다면, 사용자의 점수를 10점 증가시키고 두더지가 맞았음을 나타내는 화면을 출력  
-> try 에서 예외가 발생하면, 두더지가 나타나는 시간이 더 길어지도록 설정  

두더지가 나타난 구멍을 다시 초기화하여 숨김 상태로 만듦, 두더지가 사라진 상태의 게임 보드를 출력 후 유지  

## 6. 전체 게임 진행 함수.
```
        def play(self, user):
        self.tutorial() 
        boards.start_board() 
        while True: 
            self.play_round() 
            boards.score_board(self.points) 
            time.sleep(2.0) 
            self.cnt_round += 1 
            if (self.points != 100*(self.cnt_round-1)) and ((self.points < 100*(self.cnt_round-1)*0.8) or (self.cnt_round > 3)):
                boards.over_board() 
                break
            boards.round_board(self.cnt_round) 
            time.sleep(1.0)
        HitMole.rank[user] = self.points 
        HitMole.rank = dict(sorted(HitMole.rank.items(), key=lambda x:x[1], reverse=True)) 
        rank=1
        for name,score in HitMole.rank.items():
            print('', rank, name + ':', score, sep='\t')
            print()
            rank+=1
        time.sleep(1.0)
```
튜토리얼 진행 후 play_round 메서드를 호출하여 한 라운드 플레이  
-> 현재까지의 점수 출력 화면 보여줌(2초 동안 대기하여 점수를 확인할 시간), 라운드 수 +1   
-> 현재 라운드에서의 점수를 판별하여 게임을 계속 진행할지를 결정  
   (플레이어의 점수가 해당 라운드의 최대 가능 점수의 80% 미만이거나, 라운드 횟수가 3보다 큰 경우에는 종료 화면 후 루프 탈출)  
-> 게임 보드 출력, 현재 라운드 번호(self.cnt_round)에 해당하는 화면을 출력-> 현재 사용자의 점수를 랭킹에 내림차순 저장  




