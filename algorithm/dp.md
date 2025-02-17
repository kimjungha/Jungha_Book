## DP(Dynamic Programming) - 동적계획법

큰 문제를 작은문제로 나누어 결과를 저장하여, 동일한 작은문제를 반복해서 계산하지 않도록 하는 최적화 기법

📌 DP의 핵심 개념
1. 최적 부분 구조 (Optimal Substructure)
   * 큰 문제의 해가 작은 부분 문제의 해를 이용해 구성되는 경우
   * 예) 피보나치 수열  F(n) = F(n-1) + F(n-2)
2. 중복 부분 문제
   * 동일한 부분 문제가 여러번 반복해서 등장하는 경우 
   * 예) 피보나치 수열  F(5) = F(4) + F(3),F(4) = F(3) +F(2)

📌 DP 알고리즘 설계 방식

탑다운, 바텀업 두가지 방식으로 해결 가능
1. 탑다운(메모이제이션, memoization)
    * 재귀를 활용하여, 필요한 값만 계산하고 중복 계산을 피하기 위해 저장
    * 중복 계산을 줄이기 위해 배열을 사용하여 메모이제이션(메모화)

    ```java
    public class FibonacciDP{   
       static int[] dp = new int[50];  // 피보나치 수 저장할 배열

       public static int fib(int n) {
        if (n <= 1) return n; // 기저 조건 ( 재귀함수에서 더 이상 재귀하지 않고 종료되는 조건)
        if (dp[n] != 0) return dp[n]; // 이미 계산한 값이면 반환
        return dp[n] = fib(n - 1) + fib(n - 2); // 메모이제이션
    }

    public static void main(String[] args) {
        System.out.println(fib(10)); // 55
        }
    }

2. 바텀업 방식(점화식)
   * 작은 문제부터 차근차근 반복문을 이용하여 해결하는 방식
   * 반복문을 사용하여 배열 값을 채워가기에, 재귀호출이 없으며 스택오버플로우 위험이 없다. 

    ```java
    public class FibonacciDP {
    public static int fib(int n) {
        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = 1;
        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }

    public static void main(String[] args) {
        System.out.println(fib(10)); // 55
    }
}

📌 DP를 사용하는 대표적인 문제
1.	피보나치 수열	F(n) = F(n-1) + F(n-2)
2.	최장 공통 부분 수열 (LCS, Longest Common Subsequence)
   * 두 문자열이 주어졌을 때, 가장 긴 공통 부분 문자열을 찾는 문제
3.	배낭 문제 (Knapsack Problem)
   * 주어진 무게 제한 내에서 최대 가치를 얻을 수 있도록 아이템을 선택하는 문제
4.	최단 경로 문제 (Floyd-Warshall 알고리즘)
   * 모든 정점에서 모든 정점으로 가는 최단 거리를 찾는 문제.
5.	동전 거스름돈 문제 (Coin Change Problem)
   * 최소한의 동전 개수로 특정 금액을 만드는 문제.


📌 DP 문제 해결 4단계
1.	DP 테이블 정의: 문제를 해결하는데 필요한 배열(메모이제이션)을 정의.
2.	점화식(재귀식) 세우기: dp[i] 값을 구하는 규칙을 찾기.
3.	초기값 설정: dp[0], dp[1] 등 기저 사례를 정의.
4.	탑다운 또는 바텀업 방식으로 해결: 재귀(메모이제이션) 또는 반복문(Tabulation)으로 구현.


