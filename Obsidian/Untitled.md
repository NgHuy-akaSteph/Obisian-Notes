
![[Pasted image 20260409192251.png]]
n = int(input())
max_1 = -1
max_2 = -1
for i in range(n):
    score = int(input())
    if score > max_1:
        max_2 = max_1
        max_1 = score
    elif score > max_2 and score != max_1:
        max_2 = score

print(f"Silver = {max_2}")

![[Pasted image 20260409193626.png]]

![[Pasted image 20260409193825.png]]

def solve():  
    for k in range(int(input())):  
        s = list(input())  
        n = len(s)  
        i = n - 2  
        while i >= 0 and s[i] <= s[i + 1]:  
            i -= 1  
  
        if i < 0:  
            print("-1")  
            continue  
  
        max_val = ''  
        best_j = -1  
        for j in range(i + 1, n):  
            if s[j] < s[i]:  
                if i == 0 and s[j] == '0':  
                    continue  
                if s[j] > max_val:  
                    max_val = s[j]  
                    best_j = j  
  
        if best_j == -1:  
            print("-1")  
        else:  
            s[i], s[best_j] = s[best_j], s[i]  
            print(''.join(s))  
  
  
if __name__ == '__main__':  
    solve()

![[Pasted image 20260409195040.png]]

from collections import  deque  
  
def solve():  
    ans = []  
    q = deque(["1", "2"])  
    while len(ans) < 1000:  
        cur = q.popleft()  
        if cur.count('2') * 2 > len(cur):  
            ans.append(cur)  
        q.append(cur + "0")  
        q.append(cur + "1")  
        q.append(cur + "2")  
  
    for k in range(int(input())):  
        n = int(input())  
        print(" ".join(ans[:n]))  
  
if __name__ == '__main__':  
    solve()

![[Pasted image 20260409200429.png]]

from collections import  deque  
  
  
def find_k(n, k):  
     mid = 2 ** (n - 1)  
     if k == mid:  
         return chr(ord('A') + n - 1)  
     elif k < mid:  
         return find_k(n - 1, k)  
     else:  
         return find_k(n - 1, k - mid)  
  
def solve():  
    for i in range(int(input())):  
        n, k = map(int, input().split())  
        print(find_k(n, k))  
  
if __name__ == '__main__':  
    solve()


![[Pasted image 20260409201703.png]]
def solve():  
    for k in range(int(input())):  
        n, b = map(int, input().split())  
        if n == 0:  
            print('0')  
            continue  
        res = ''  
        while n > 0:  
            rem = n % b  
            if rem < 10:  
                res += str(rem)  
            else:  
                res += chr(ord('A') + rem - 10)  
            n //= b  
        print(res[::-1])  
  
if __name__ == '__main__':  
    solve()


![[Pasted image 20260409204312.png]]

def solve():  
    s = input().strip()  
    if s.startswith('-'):  
        s = s[1:]  
  
    if len(s) == 1:  
        print(1)  
        return  
  
    steps = 0  
    while len(s) > 1:  
        total = sum(map(int, s))  
        s = str(total)  
        steps += 1  
  
    print(steps)  
  
  
if __name__ == '__main__':  
    solve()