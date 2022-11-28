## 최종 결과 설명  

### 코드 실행 순서  
  
0. FINAL_SUBMISSION/npy_60000/train, FINAL_SUBMISSION/npy_60000/valid, FINAL_SUBMISSION/npy_60000/test, FINAL_SUBMISSION/results 폴더를 생성합니다.  
1. convert_npy.ipynb를 통해서 기존 데이터를 60000 resampling 하고 이를 저장하는 과정을 거칩니다. 코드 블록을 순차적으로 실행하시면 됩니다. (단, 경로 상에 폴더가 존재하는지 확인 부탁드립니다. 예를 들어, npy_60000/train 폴더가 없는 경우 에러가 발생하오니 해당 폴더를 만들어주시길 바랍니다.)  
2. FINAL_TRAIN_EVAL.ipynb에는 train 코드와 inference 코드가 동시에 존재합니다.  

### 추가 데이터 사용 시 사용 방법  
0. FINAL_SUBMISSION/npy_60000/ 경로에 폴더를 하나 생성합니다. (또는 test 폴더에 기존 데이터를 넣어두셨다면 상관 없습니다.)  
1. convert_npy.ipynb의 test 데이터를 만드는 것을 참고하여서 동일하게 60,000 resampling 및 npy 변환 저장을 진행합니다.  
2. FINAL_TRAIN_EVAL.ipynb를 통해서 train 또는 inference를 진행하시면 됩니다. (inference는 학습을 하는 코드를 제외하고 사용하시면 됩니다.)  


### 코드 설명

1. 시작 전에 제공된 requirements.txt를 설치합니다.  

< convert_npy.ipynb 설명 >  
0번 문단: 필요한 library를 import 합니다.
1번 문단: seed 고정을 위한 코드이며 seed를 고정합니다.  
2번 문단: data가 존재하는 경로를 입력하고, npy로 변환한 데이터가 저장 될 경로를 입력합니다.
3번 문단: 학습 data 파일들의 label을 얻고, train과 validation으로 분할합니다.
4번 문단: edf 파일을 npy 파일로 변환하는 함수를 정의합니다.
5번 문단: train과 validation 파일들을 모두 60,000으로 resampling 및 npy로 변환하여 저장합니다.
6번 문단: test 파일들을 모두 60,000으로 resampling 및 npy로 변환하여 저장합니다.

< FINAL_TRAIN_EVAL.ipynb 설명 >  
0번 문단: requirements.txt를 설치합니다.  
1번 문단: 필요한 library를 import 합니다.  
2번 문단: seed 고정을 위한 코드이며 seed를 고정합니다.  
  
3번 문단: data가 존재하는 파일 경로를 입력합니다.  
4번 문단: data가 존재하는 파일 경로를 "file_name".npy 까지 포함하는 list를 생성합니다.  
5번 문단: npy data를 불러오는 dataset class를 선언합니다. (이름은 EDFDataLoader입니다.)  
6번 문단: Dataset과 DataLoader를 정의합니다.  

7번 문단: DeepSleepNet 모델을 선언합니다. DeepSleepNet 모델에는 BiLSTM도 필요하므로 같이 선언합니다.  
8번 문단: FocalLoss를 선언합니다.  
9번 문단: Model, Loss, Optimizer, Scheduler 등을 모두 입력받습니다.  
  
10번 문단: 학습을 진행합니다. (이 때, validation에 대한 결과도 같이 출력됩니다.)  

11번 문단: test data에 대한 Dataset, DataLoader를 정의하고, pth model을 불러옵니다.  
12번 문단: inference를 진행합니다.  
13번 문단: inference 결과를 출력하고 csv로 저장합니다.  


### 주의 사항  
- 코드 시작 전 데이터 셋 경로를 바꾸신 경우 맞춰주세요.  
- 본 FINAL_TRAIN_EVAL.ipynb에는 train과 inference가 같이 존재합니다.  
- 만약 inference만 사용하고자 하시는 경우, 학습을 진행하는 부분을 제외하고 실행해주시면 됩니다.  
- 해당 코드에는 외부 데이터 및 weight가 사용되지 않았습니다. (다만, 외부에서 참고한 코드는 사용되었습니다. ex. FocalLoss / Reference는 코드 블록 시작 란에 적어두었고 license에 허락되는 코드를 사용하였습니다.)    