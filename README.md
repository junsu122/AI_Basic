# AI_Basic
- 두산 루키 7키
- AI 기초 정리
- Colab 사용
- 예제 파일 적극 활용


## 폰트 설정 (Colab 한글 깨짐 방지)
코랩 환경에서 matplotlib 사용 시 한글 깨짐 현상을 해결하기 위해 아래 명령어를 실행하세요.

```bash
!sudo apt-get install -y fonts-nanum* | tail -n 1
!sudo fc-cache -fv
!rm -rf ~/.cache/matplotlib
```

## 필요 라이브러리 설치
```bash
!pip install torchviz | tail -n 1
# 코랩 기준, 세션 다시 실행!!
```

## 라이브러리 임포트 및 글꼴 설치
```bash
# 라이브러리 임포트
%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt
from IPython.display import display

# 폰트 관련 용도
import matplotlib.font_manager as fm

# 나눔 고딕 폰트의 경로 명시
path = '/usr/share/fonts/truetype/nanum/NanumGothic.ttf'
font_name = fm.FontProperties(fname=path, size=10).get_name()
```
```bash
# 기본 폰트 설정
plt.rcParams['font.family'] = font_name

# 기본 폰트 사이즈 변경
plt.rcParams['font.size'] = 14

# 기본 그래프 사이즈 변경
plt.rcParams['figure.figsize'] = (6,6)

# 기본 그리드 표시
# 필요에 따라 설정할 때는, plt.grid()
plt.rcParams['axes.grid'] = True

# 마이너스 기호 정상 출력
plt.rcParams['axes.unicode_minus'] = False

# 넘파이 부동소수점 자릿수 표시
np.set_printoptions(suppress=True, precision=4)
```
