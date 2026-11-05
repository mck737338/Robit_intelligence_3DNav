
## 작성한 launch 파일

```python

import os

from ament_index_python.packages import get_package_share_directory
from launch import LaunchDescription
from launch_ros.actions import Node


def generate_launch_description():
    params = os.path.join(get_package_share_directory('turtle_adv'),
                          'config', 'follow_params.yaml')

    return LaunchDescription([
        Node(package='turtlesim', executable='turtlesim_node',
             name='sim'),

        Node(package='turtle_adv', executable='pose_broadcaster',
             name='broadcaster1', parameters=[{'turtlename': 'turtle1'}]),

        Node(package='turtle_adv', executable='pose_broadcaster',
             name='broadcaster2', parameters=[{'turtlename': 'turtle2'}]),

        Node(package='turtle_adv', executable='turtle_follower',
             name='turtle_follower', parameters=[params]),
    ])
```

- 좌표계 발행 노드를 두 개 띄웠다. 두 거북이가 모두 화면 좌표계에 매달려 있어야 서로의 상대 위치를 뽑을 수 있다.
- 같은 프로그램을 두 번 띄우므로 이름을 다르게 붙였다. 과제 2에서 구역 이름이 하던 역할을 여기서는 노드 이름이 맡는다.
- 쫓기는 거북이를 만드는 일은 쫓아가기 노드가 직접 하므로 launch에 넣지 않았다.


## 작성한 설정 파일

```yaml
turtle_follower:
  ros__parameters:
    k_ang: 4.0   # 방향을 트는 세기
    k_lin: 0.5   # 다가가는 세기
```

## 결과

[hw4-1](https://drive.google.com/file/d/1Vpph1N0LyNjdNOigozX8rTN_sVEkWTCo/view?usp=sharing)

- 명령 한 번으로 네 개 노드가 모두 뜨는 것을 확인함.
- 쫓기는 거북이가 지정한 자리에 생성되는 것을 확인함.
- 앞 거북이를 조종하면 뒤 거북이가 따라오는 것을 확인함.
- 설정 파일에 적은 값이 노드에 그대로 들어간 것을 확인함.

[hw4-2](https://drive.google.com/file/d/1aQWso8eqHuLvo45j4VuUTxhwjSpY7cKd/view?usp=sharing)

- 좌표계 구조에서 두 거북이가 모두 화면 좌표계를 부모로 두고 있는 것을 확인함.
- 회전 명령을 따로 내리는 동안에도 쫓아가기가 끊기지 않는 것을 확인함. 다만 두 거북이가 이미 붙어 있으면 앞 거북이가 제자리 회전만 할 때 뒤 거북이는 거의 움직이지 않았다. 쫓아가기가 상대의 위치만 쓰고 방향은 보지 않기 때문이다.

---

# 파라미터에 따른 궤적 비교

설정 파일의 두 값을 바꿔 가며 다시 실행하고, 매번 펜 자국을 지운 뒤 앞 거북이를 비슷한 경로로 끌고 다녔다. 쫓는 거북이는 항상 같은 자리에서 출발하므로 조건이 같다.

화면에 남는 선은 두 줄이다. **각진 선**이 조종한 거북이의 경로, **부드러운 선**이 쫓아간 거북이의 궤적이다. 두 선이 얼마나 겹치는지를 봤다.

## 방향을 트는 세기

[param_1.0_0.5](https://drive.google.com/file/d/16Oa3s-oPcebZQ0Q-_X-c2mnpYZc0SDAd/view?usp=sharing)

[param_4.0_0.5](https://drive.google.com/file/d/1C42EQe3Z6blg-eIkhwxsugTlM7G_UDwb/view?usp=sharing)

[param_8.0_0.5](https://drive.google.com/file/d/1wA_IeQfZry1OVSrQtq11vdD-oUPAtGe3/view?usp=sharing)

| k_ang | k_lin | 궤적 |
|---:|---:|---|
| 1.0 | 0.5 | 모서리를 크게 질러간다. 꺾이는 지점마다 바깥으로 부풀어 두 선이 뚜렷이 벌어진다. |
| 4.0 | 0.5 | 꺾이는 지점에서 거의 제자리에서 몸을 돌려 경로를 덧그린다. 두 선이 겹쳐 이중선처럼 보인다. |
| 8.0 | 0.5 | 4.0과 눈으로 구분하기 어렵다. |

- 1.0에서 4.0으로 올릴 때는 차이가 확연한데 그 위로는 거의 달라지지 않는 것을 확인함.

## 다가가는 세기

[param_4.0_0.2](https://drive.google.com/file/d/1FCG2PGoPTm2Vc5Vkkp7UyX_ZJv8WwnPb/view?usp=sharing)

[param_4.0_1.0](https://drive.google.com/file/d/1biL6Tsy4YFHUGYB5y6npoLVzR_jCvSrW/view?usp=sharing)

[param_4.0_2.0](https://drive.google.com/file/d/1lh-5y1QAjLZce4GjK7ZDfewGVdStr4Yv/view?usp=sharing)

| k_ang | k_lin | 궤적 |
|---:|---:|---|
| 4.0 | 0.2 | 선 모양은 거의 그대로이고 간격만 넓게 벌어진 채 따라온다. |
| 4.0 | 1.0 | 더 바짝 붙는다. 모서리에서 약간 부푼다. |
| 4.0 | 2.0 | 거의 붙어 다닌다. 속도가 빨라 벽에 부딪히기도 했다. |

- 궤적의 모양은 거의 건드리지 않고 따라붙는 거리만 달라지는 것을 확인함.

