# 실습 2 보고서 — SLAM (지도 만들기)
**예비단원 김민찬**
**스크립트**: `scripts/lab2_slam.sh`

## 설정

사전 지도 없이 시작하므로 lab1과 달리 2D Pose Estimate 과정이 없음. 

## 진행

Nav2 Goal로 미탐색(회색) 영역 방향을 지정해 로봇을 이동시키며 지도를 확장함.

## 결과

[과제2 영상](https://drive.google.com/file/d/1e8uX6eCBV5nvL_qVI0XVtriXIyLrsM0M/view?usp=sharing)

로봇이 이동할수록 흰색(빈 공간)과 검정(벽) 영역이 넓어지며 지도가 실시간으로 갱신되었음


최종적으로 육각형 외벽 전체와 원기둥 9개가 모두 맵핑됨

SLAM 진행 중에도 Nav2 주행이 정상적으로 주행함.

