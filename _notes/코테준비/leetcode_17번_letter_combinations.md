---
---

# LeetCode 17. Letter Combinations of a Phone Number 문제 정의 및 풀이 코드 해설

## 1. 문제 정의

LeetCode 17번 **Letter Combinations of a Phone Number** 문제는 숫자 문자열 `digits`가 주어졌을 때, 각 숫자가 휴대폰 키패드에서 의미하는 문자들을 이용해서 만들 수 있는 **모든 문자 조합**을 구하는 문제이다.

휴대폰 키패드의 숫자와 문자의 대응 관계는 다음과 같다.

```python
phone = {
    "2": "abc",
    "3": "def",
    "4": "ghi",
    "5": "jkl",
    "6": "mno",
    "7": "pqrs",
    "8": "tuv",
    "9": "wxyz"
}
```

단, 문제에서 요구하는 중요한 조건은 다음과 같다.

- 입력 문자열 `digits`는 숫자 `2`부터 `9`까지만 포함한다.
- 각 숫자는 여러 개의 알파벳 문자와 대응된다.
- 가능한 모든 문자 조합을 리스트 형태로 반환해야 한다.
- 반환 순서는 상관없다.
- 1<= `digits`의 길이 <=4

예제 Input

```python
digits = "23"
```
예제 Output
```python
["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]
```


## 2. 풀이 아이디어
```text
숫자 문자열을 리스트로 바꾼다.
각 숫자를 문자 리스트로 치환한다.
첫 번째 문자 리스트를 Output으로 둔다.
두 번째 문자 리스트부터 Output과 조합한다.
조합된 결과를 다시 Output에 저장한다.
마지막 Output을 반환한다.
```

## 3. 풀이 코드

```python
class Solution(object):
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """

        phone = {
            "2": "abc",
            "3": "def",
            "4": "ghi",
            "5": "jkl",
            "6": "mno",
            "7": "pqrs",
            "8": "tuv",
            "9": "wxyz"
        }

        if digits == "":
            return []

        InputNum = list(digits)

        for i in range(len(InputNum)):
            InputNum[i] = list(phone[InputNum[i]])

        Output = InputNum[0]

        for i in range(1, len(InputNum)):
            Temp = []

            for out in Output:
                for ch in InputNum[i]:
                    Temp.append(out + ch)

            Output = Temp

        return Output
```
문제 풀이에 용이하게 digits를 가공하여
반복문을 활용하여 남은 입력의 경우의 수에 맞게 늘려간다.
핵심은 데이터가공과 3중 반복문이다.

이 3중 반복문의 데이터는 처음 입력되는 숫자의 경우의 수를 기반으로 하여 후에 입력되는 문자의 경우의 수들을 전부 추가하는 형식이다.
