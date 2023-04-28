# LG-AImers-Hackaton
2023년 2월동안 진행한 Dacon 대회 참여 기록
![LG AI.pdf](https://github.com/uvictoli/LG-AImers-Hackaton/files/11350091/LG.AI.pdf)

***
## 스마트 공장 제품 품질 상태 분류 AI 온라인 해커톤  
https://dacon.io/competitions/official/236055/overview/description
#### [배경]  
팬데믹을 맞이한 최근 몇 년간 제조 운영과 공급망의 디지털 혁신은 관련 사업 분야에서 최우선 과제로 급부상했습니다.  
스마트 공장은 공정 데이터에서 인사이트를 발굴하고 해석하여 추세를 예측하고, 스마트 제조 워크플로와 자동화된 프로세스를 구현합니다.  
<br>
LG에서는 제조 지능화를 통해 공정 과정에서 발생하는 이벤트에 신속하게 대응하고, 안정선과 효율을 극대화하기 위한 방안을 지속적으로 도모하고 있습니다. 품질 편차를 최소화해 생산 경제성과 안정성을 확보할 수 있도록 생산된 제품이 적정 기준을 충족하는지 판단하고 분유하는 AI 모델을 개발해 주세요.
<br>
<br>
#### [주제]
스마트 공장의 제어 시스템 구축을 위한 제품 품질 분류 AI 모델 개발
<br>
<br>
#### [설명]
실제 스마트 공장 데이터를 기반으로 제품의 품질 상태를 분류하는 AI 모델을 개발하세요.  
  
온라인 해커톤(Phase2)에서 교육생들의 문제 해결 능력을 검증하여 오프라인 해커톤(Phase3)에 진출할 30팀을 선발하기 위한 과정입니다.  
  
단, 오프라인 해커톤(Phase3) 진출할 30팀의 총 인원이 100명 미달 시, 추가 선발 가능  
오프라인 해커톤(Phase3)은 1박 2일간 오프라인으로 진행되며, 온라인 해커톤(Phase2)과 주제는 동일합니다.  
<br>
<br>
#### [주최/주관]
주최 : LG AI Research  
주관 : 데이콘
<br>
<br>
#### [참가 자격]
LG Aimers 교육생  
※ 참여 버튼을 누른 뒤 팝업 창에서 성명, LG Aimers 메일을 기재  
※ 데이콘 계정 메일과 LG Aimers 메일이 일치할 필요 없음  
※ 참여 관련 문제가 있는 LG Aimers 교육생의 경우 dacon@dacon.io로 문의  
<br>
***
## Solution
0. 데이터 전처리  
feature가 너무 많아 각 feature간 연관성, 상관관계 파악이 어려움  
→ PCA 등으로 feature의 개수를 줄이자  
⇒ 데이터를 통째로 집어넣고 RF 실행 ⇾ importance가 일정 기준 이하인 feature 삭제하는 방식 선택  
<br>

1. 공정 시각 시계열 데이터 처리    
시계열 데이터를 변환할 수 있는 방법 중 '퓨리에 변환' 선택 ⇾ 시계열 데이터 유무가 정확도 향상에 큰 영향이 없음을 판단    
→ 많은 feature 중 시계열과 관련된 feature가 있을 것이라 예상    
⇒ 시계열 데이터는 아예 제외하고 남은 feature 중 공정 시각과 관련 있는 feature를 찾아보자  
<br>

2. 모델  
- Random Forest  
∵ 정형데이터의 경우 Tree 구조의 모델에서 좋은 성능을 보인다는 논문 참고    
⇒ 데이터를 통째로 넣어 RF 1차 실행 ⇾ importance가 낮은 feature를 삭제하고 다시 RF 2차 실행  
\+ RF를 여러 번 할수록 불필요한 feature가 줄어들면서 정확도가 올라갈 것으로 예상했으나 2번까지 실행했을 때 가장 성능이 좋았음   

- LSTM

- AutoML
  - "Y_Quality"를 제외하고 AutoML Classification 실행
  - AutoML Regression으로 "Y_Quality"를 먼저 예측하고 이를 기반으로 "Y_Class" 예측

