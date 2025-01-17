# day12
import sys
from itertools import combinations

# N 입력
N = int(sys.stdin.readline())

# power 배열 입력
power = [list(map(int, sys.stdin.readline().split())) for _ in range(N)]

# 사람들의 번호 리스트
people = list(range(N))

# 가능한 모든 스타트 팀을 구하기 위한 조합
combi = list(combinations(people, N // 2))

# 능력치 차이의 최솟값을 구하기 위한 변수
min_diff = sys.maxsize

# 조합을 하나씩 처리하여 팀을 나누고 능력치 차이를 계산
for start_team in combi:
    start_team = set(start_team)  # 스타트 팀을 set으로 변환
    link_team = set(people) - start_team  # 나머지 사람들은 링크 팀

    # 스타트 팀의 능력치 계산
    start_score = 0
    for i, j in combinations(start_team, 2):
        start_score += power[i][j] + power[j][i]

    # 링크 팀의 능력치 계산
    link_score = 0
    for i, j in combinations(link_team, 2):
        link_score += power[i][j] + power[j][i]

    # 능력치 차이 계산
    diff = abs(start_score - link_score)

    # 최솟값 갱신
    min_diff = min(min_diff, diff)

# 결과 출력
print(min_diff)
