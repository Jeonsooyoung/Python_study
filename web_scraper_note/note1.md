# 1 THEORY (이론)
## 1. Data Type
- 변수 선언 :  <br>
              (number) a = 2, b = 3.12,    
              (text) c = "3",     
              (boolean) c = True,  d = False     
              (none) e = None (존재하지 않음)    
              
- 타입 표시 : print(type + (변수명) )
- variable type : 숫자, 문자, 참.거짓, null 값
- python 변수 컨벤 션 : snake case (ex) super_long_variable 


## 1.1 List in Python 
There is two sequence type  in python. one is list the other one is tuple.

하나의 변수에 여러개의 값을 넣고 싶을 때, 문자열로 저장할 경우, 데이터를 추가하거나, 각 데이터 값을 추출할 때 어려움.<br>
=> list 를 사용

- day = ["Mon", "Tue"] : 대괄호로 정의
- 파이썬 공식 문서에 리스트에 사용할 수 있는 연산자 있음.    
URL : https://docs.python.org/3/library/     
https://docs.python.org/3/library/stdtypes.html#sequence-types-list-tuple-range    


## 1.2 Tuples and Dicts
1) Tuple
- days = ("Mon","Tue") 
- 아무도 변경 할 수 없는 리스트
- sequence를 변경 할 수 없음 
- list 와 같은 연산자 사용 가능 (50% 정도)
2) Dict 
-사전과 같이 key- value 로 이루어진 list 
person = {
  "name":"sooo",
  "age":15,
  "korean":True,
  "fav_food":["Cake","rice"]
}

print(person)
person["happy"] = True
print(person)

## 1.3 Built in Functions
function : 반복해서 사용할 수 있는 기능을 정의 
built in function : 파이썬에서 미리 정의된 함수. 언제나 사용 가능함(always available)
<br>
1) abs(x) : Return the <u>absolute value</u> of a number.<br>
The argument may be an integer, a floating point number(소수점 수), or an object implementing __abs__(). If the argument is a complex number(복소수?), its magnitude(크기) is returned.
<br><br>
2) all(iterable)<br>
* iterable 객체 - 반복 가능한 객체 <br>
* 대표적으로 iterable한 타입 - list, dict, set, str, bytes, tuple, range <br>
Return True if all elements of the iterable are true (or if the iterable is empty).
<br><br>
3) any(iterable)¶<br>
Return True if any element of the iterable is true. If the iterable is empty, return False.
<br><br>
4) ascii(object)



# 1.4 Creating a Your First Python Function     
define a function     
def 로 함수 정의     
def say_hello () :     
  print ("hello")    
  
- 파이썬은 중괄호로 함수의 시작과 끝을 판단하지 않음.    
indentation(들여쓰기로) function의 안을 표시함.(보통tab키로 들여씀)    
- 함수 명 뒤에 괄호를 추가하면 function을 실행함    


# 1.5 Function Arguments (positional arguments)
- print도 function 중 하나임. print function은 괄호 안에 뭔가 넣는 것을 허용한다.       
function 에 data의 input 된 data가 필요할 경우가 있기 때문       
함수를 정의할 때 function 이름을 정의하고, 괄호 안에 뭔가를 넣을 수 있도록 허용해야한다.    
그리고 function 이 가질 수 있는 arguments(인자)에 이름을 지어줄 수 있음.    

<code>
  def say_hello(who) : 
    print("hello", who)
</code>

- arguments에 기본값을 추가할 수 있음. 


# 1.6 Returns
-function의 결과물. 반환값을 의미    
return 하는 순간 해당 함수는 종료됨. 함수 내에서 return 은 한번만 실행됨. 

-예제에서 사용한 print함수는 결과를 단순 console에만 출력함    
이는 print로 함수를 호출할 경우, 해당 함수 안에 return  값이 아닌 print 함수가 있으면 
아무런 결과 출력 되지 않음 ex) 
def p_plus(a,b) : 
  print(a+b)
  
p_result = p_plus(2,3)
print(p_result)

# 1.7 Keyworded Arguments
- 인자인데, 위치가 아닌 arguments의 이름으로 쌍을 이루어줌    
인자의 순서를 신경 쓸 필요가 없고, 인자의 이름만 신경써주면 됨. 
- string 안에 변수를 포함시키고 싶으면 따옴표 가장 앞에 f(format)를 추가하고 변수의 이름에 중괄호 감싸주기     
문자열끼리 + 를 이용해서 연결할 수 있음. 


<code>
def p_plus(a=1,b=2) : 
  print(a+b)
</code>

# 1.8 Code Challenge (계산기)
- 7가지 function 만들기 
plus(+), minus(-), times(*), division(/), negation(//), power(**) , reminder(%)<br> 

- 숫자뿐 아니라 문자열 타입이 추가될 수도 있음 (오류체크)

# 1.9 Conditionals part One
- if-else 조건문을 통해서 string 값에는 다른 문구 출력    
- 조건문에 True라는 조건을 주게 되면 조건이 참이되는 결과를 실행
- type(변수명) is str : 변수의 타입이 문자열이라면    


# 1.10 if else and or
- 조건문에는 boolean operation 사용. or(둘중 하나만 true), and(둘다 true), not(조건이 false) 이 있음.    

# 1.11 for in
- 반복문. 뭔가를 순차적으로 작업해야할 때, 사용
<code>
  for x in days :       
 </code>
 여기서 x는 작업되는 배열의 item을 가르킴    
 for문을 진행하다가 특정 조건에서 break되도록 하면 해당코드에서 실행이 중단됨 
 - <strong>파이썬에서는 string 도 배열임. for문 (string, tuple, list)를 돌릴 수 있음.</strong>    
  
# 1.12 Modules
- 파이썬에서는 Modules라는 것이 내장되어있음.   
기능의 집합인데, 임포트 해서 사용할 수 있음.   
기본으로 제공하는 Module은 모듈을 따로 설치할 필요없이 import하면 함수를 사용할 수 있음.   
ex) import math ,  import datetime    

- 모듈 전체를 불러오는 것은 비효율적. 모듈 내 해당하는 기능만 import하는 것이 좋음    
ex) from math import ceil ( math모듈 내, ceil 기능만 임포트)     

- 임포트한 모듈의 이름변경 가능 
ex) from math import ceil as basic_sum     

- 다른 파일에서 정의된 함수(기능)을 임포트 할 수 있음.    
ex) from calculator(파일명, .py샐약 가능)impport plus(기능명)     




