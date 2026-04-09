
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

