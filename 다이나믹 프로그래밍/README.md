# :book: 다이나믹 프로그래밍

## 다이나믹 프로그래밍

- 메모리를 적절히 사용하여 수행 시간 효율성을 비약적으로 향상시키는 방법
- **이미 계산된 결과(작은 문제)는 별도의 메모리 영역에 저장하여 다시 계산하지 않도록 합니다.**
- 다이나믹 프로그래밍의 구현은 일반적으로 두 가지 방식(탑다운과 보텀업)으로 구성
- 동적 계획법이라고도 부른다
- 일반적인 프로그래밍 분야에서의 동적이란?
  - *자료구조에서 동적 할당은 프로그램이 실행되는 도중에 실행에 필요한 메모리를 할당하는 기법*
  - 반면에 다이나믹 프로그래밍에서 다이나믹은 **별다른 의미 없이 사용**
- 다이나믹 프로그래밍은 문제가 다음의 조건을 만족할 때 사용
  - **최적 부분 구조**
    - 큰 문제를 작은 문제로 나눌 수 있으며 작은 문제의 답을 모아서 큰 문제를 해결
  - **중복되는 부분 문제**
    - 동일한 작은 문제를 반복적으로 해결

### 피보나치 수열

- `1,1,2,3,5,8,13,21,34,55,89...`
- 점화식이란 인접한 항들 사이의 관계식을 의미
- 피보나치 수열을 점화식으로 표현하면 다음과 같다
  - An=An-1+An-2, A1-1,A2=1

![피보](https://user-images.githubusercontent.com/47052106/105494636-6de36600-5cfe-11eb-9fba-349ef9d91c61.JPG)

![11](https://user-images.githubusercontent.com/47052106/105494631-6cb23900-5cfe-11eb-9368-dcd6bf11286b.JPG)

```python
# 재귀
def fibo(x):
  if x==1 or x==2:
    return 1
  return fibo(x-1) + fibo(x-2)
```

![시간복잡](https://user-images.githubusercontent.com/47052106/105494879-c7e42b80-5cfe-11eb-8e98-6f2bcbf7a050.JPG)

![시간](https://user-images.githubusercontent.com/47052106/105495196-36c18480-5cff-11eb-9fd8-ffbbf665574b.JPG)

### 피보나치 디피를 사용하자

![디피](https://user-images.githubusercontent.com/47052106/105495361-6f615e00-5cff-11eb-9af9-4cecce9877af.JPG)

- **메모이제이션**
  - 메모이제이션은 다이나믹 프로그래밍을 구현하는 방법 중 하나
  - 한번 계산된 결과를 메모리 공간에 메모하는 기법
    - 같은 문제를 다시 호출하면 메모했던 결과를 그대로 가져옴
    - 값을 기록해 놓는다는 점에서 캐싱이라고도 한다

![탑다운](https://user-images.githubusercontent.com/47052106/105495699-d4b54f00-5cff-11eb-906d-97cb2f7869b2.JPG)

- 탑다운
  - 재귀
- 보텀업
  - 반복문

```python
# 탑다운 디피
# 한번 계산된 결과를 메모이제이션하기 위한 리스트 초기화
d = [0] * 100

# 피보나치 함수를 재귀함수로 구현 (탑다운 디피)

def fibo(x):
  # 종료 조건
  if x ==1 or x==2:
    return 1
  # 이미 계산한 적 있는 문제라면 그대로 반환
  if d[x]!=0:
    return d[x]
  # 아직 계산하지 않은 문제라면 점화식에 따라서 피보나치 결과 반환
  d[x] = fibo(x-1)+fibo(x-2)
  return d[x]
  
# 보텀업 방식

d = [0] * 100

d[1]=1
d[2]=1
n=99

for i in range(3,n+1):
  d[i]=d[i-1]+d[i-2]
```

![메모이동작](https://user-images.githubusercontent.com/47052106/105496732-39bd7480-5d01-11eb-81ac-2cc0ae0a1e1f.JPG)

![맴ㅎ아뷴속](https://user-images.githubusercontent.com/47052106/105497009-9caf0b80-5d01-11eb-8fd2-8db0be979635.JPG)

### 다이나믹 프로그래밍 vs 분할 정복

- 다이나믹 프로그래밍과 분할 정복은 모두 최적 부분 구조를 가질 때  사용
  - 큰 문제를 작은 문제로 나눌 수 있으며 작은 문제의 답을 모아서 큰 문제를 해결할 수 있는 상황
- 다이나믹 프로그래밍과 분할 정복의 차이점은 **부분 문제의 중복**
  - 다이나믹 프로그래밍 문제에서는 각 부분 문제들이 서로 영향을 미치며 부분 문제가 중복
  - 분할 정복 문제에서는 동일한 부분 문제가 반복적으로 계산되지 않는다

![분할](https://user-images.githubusercontent.com/47052106/105497355-10511880-5d02-11eb-97d3-c26875b021c4.JPG)

![접근](https://user-images.githubusercontent.com/47052106/105497466-3971a900-5d02-11eb-8051-93bb8022788f.JPG)

## 문제

### 개미전사

![개미전사](https://user-images.githubusercontent.com/47052106/105513908-3da7c180-5d16-11eb-8352-d30f1e52ef51.JPG)

![문제](https://user-images.githubusercontent.com/47052106/105513911-3f718500-5d16-11eb-8402-4ceba9613492.JPG)

![조건](https://user-images.githubusercontent.com/47052106/105513912-400a1b80-5d16-11eb-83b4-d760b010136e.JPG)



