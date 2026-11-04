# 실습 3 보고서 — 파라미터 튜닝
**예비단원 김민찬**

**스크립트**: `scripts/lab3_params.sh`
**설정 파일**: `params/nav2_params.yaml`

## 수정한 파라미터

`### [LAB3]` 주석이 붙은 두 항목을 변경하며 비교했습니다.

| 파라미터 | 시험한 값 |
|---|---|
| `inflation_radius` | 0.30 / 0.70(기본) / 1.00 |
| `FollowPath.plugin` | MPPI(기본) → Regulated Pure Pursuit |

## 시험 조합

| 영상 | 컨트롤러 | `inflation_radius` | 검증 방식 |
|---|---|---|---|
| lab3_default | MPPI | 0.70 (기본) | RViz Nav2 Goal |
| lab3_mppi_0.3 | MPPI | 0.30 | RViz Nav2 Goal ×3 |
| lab3_mppi_1.0 | MPPI | 1.00 | RViz Nav2 Goal ×3 |
| lab3_rpp_0.3 | RPP | 0.30 | lab4 웨이포인트 순회 |
| lab3_rpp_0.7 | RPP | 0.70 | RViz Nav2 Goal |

## 결과 1 — 팽창 반경에 따른 맵 변화

[기본](https://drive.google.com/file/d/1TwAnth1uEdNrJR6MjD25to6s2-XpU6Vj/view?usp=sharing)

[MPPI 0.3](https://drive.google.com/file/d/1WxtbRBcUltzN5BUu1sSbKAZv1ZDGG-i6/view?usp=sharing)

[MPPI 1.0](https://drive.google.com/file/d/1EAUDF9ZaBfpODkWk573lQuYwWfEs4iCP/view?usp=sharing)


| `inflation_radius` | 비교 |
|---|---|
| 0.30 | 기둥 사이에 흰색 통로가 남음 |
| 0.70 (기본) | 내부 전체가 팽창 비용으로 덮임 |
| 1.00 | 0.70과 거의 동일 |

0.30에서만 기둥 사이에 비용 0 통로가 유지되며, 경로가 장애물에 비교적 가깝게 지나갑니다. 0.70 이상에서는 자유 공간이 사라지고 경로가 벽에서 더 떨어집니다.

## 결과 2 — 컨트롤러 비교

[RPP 0.7](https://drive.google.com/file/d/1adk265Jr6hlP3Z3kR38X8DYo4HbEyxsh/view?usp=sharing)

[RPP 0.3](https://drive.google.com/file/d/13neHA1xQbxCN-101fwggNEU9LtLB0h9O/view?usp=sharing)
