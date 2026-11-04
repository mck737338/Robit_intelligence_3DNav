# 실습 1 보고서 — 기본 내비게이션 

**예비단원 김민찬**

**스크립트**: `scripts/lab1_basic.sh`

## 설정

파라미터 수정 없이 `nav2_bringup`의 기본값으로 진행

## 진행

1. Gazebo와 RViz 기동
2. RViz **2D Pose Estimate**로 로봇 실제 위치(약 x = −2.0, y = −0.5)를 지정하고 +x 방향으로 드래그
3. **Nav2 Goal**로 목표 지점 지정

## 결과

[과제1 영상](https://drive.google.com/file/d/1b5LeLWRWvFnKs_m8hRXKH2koB-dbz_fi/view?usp=sharing)

초기 위치를 지정하기 전에는 `map` 프레임이 없어 RViz에 "Global Status: Error"가 표시되었고, 초기 위치 지정 직후 에러 출력이 없어지고 정상 동작함
