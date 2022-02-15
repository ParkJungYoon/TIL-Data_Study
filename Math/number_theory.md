> **Elice  Ai Track**에서 제공하는 강의자료를 바탕으로 작성하였습니다.  

# 프로그래밍 수학
## 1. 정수론: 소수

### < 에라토스테네스의 체 >
: 체를 통해 고운 입자만 통과시키는 것처럼 주어진 범위의 수 중에서 소수만을 남기는 방법

1. 찾고자 하는 범위의 자연수를 나열한다.
2. 2부터 시작하여, 2의 배수를 지워나간다.
3. 다음 소수의 배수를 모두 지운다.

* 코드 예시
    * n보다 작은 모든 소수의 리스트를 구하는 함수
    ```python
    def eratosthenes(n):
    # True는 소수, False는 합성수를 의미
    sieve = [True] * n
    
    for i in range(2, n):
        for j in range(i+i,n,i):
            sieve[j] = False

    return [i for i in range(2,n) if sieve[i] == True]
    ```

### < 소인수분해 >

* 코드 예시
    * 주어진 n에 대해 가장 큰 소인수를 구하는 함수
    ```python
    # n도 소수가 될 수 있기 때문에 0부터 n+1까지 True 리스트 만들고
    def greatPrimeFacter(n):
        sieve = [True] * (n+1)

        for i in range(2, n+1):
            if sieve[i] == True:
                for j in range(i+i, (n+1), i):
                    sieve[j] = False

    # n보다 작은 소수    
        prime_list = [i for i in range(2,n+1) if sieve[i] == True]

    # n보다 작은 소수 중에서 가장 큰 n의 인수
        return max([p for p in prime_list if n%p == 0])
    ```
    <br>

    * 주어진 수 n을 소인수분해하는 함수
    ```python
    # n 보다 작은 모든 소수의 리스트를 반환
    def eratosthenes(n):
        sieve = [True] * n
        for i in range(2, n):
            if sieve[i] == True:
                for j in range(i+i, n, i):
                    sieve[j] = False                
        return [ i for i in range(2,n) if sieve[i] == True]


    def primeFactor(n):
        l = eratosthenes(n+1)
 
        i = 0
        result = []
        while i < len(l): 
            if n % l[i] == 0:
                result.append(l[i])
                n = n // l[i]
            else:
                i += 1
        
        return result
    ```
