
# 🏆 Recyclables Object Detection

<br />

## ✏️ Introduction
바야흐로 대량 생산, 대량 소비의 시대. 우리는 많은 물건이 대량으로 생산되고, 소비되는 시대를 살고 있습니다. 하지만 이러한 문화는 '쓰레기 대란', '매립지 부족'과 같은 여러 사회 문제를 낳고 있습니다. 분리수거는 이러한 환경 부담을 줄일 수 있는 방법 중 하나입니다. 잘 분리배출 된 쓰레기는 자원으로서 가치를 인정받아 재활용되지만, 잘못 분리배출 되면 그대로 폐기물로 분류되어 매립 또는 소각되기 때문입니다.
따라서 우리는 사진에서 쓰레기를 Detection 하는 모델을 만들어 이러한 문제점을 해결해보고자 합니다. 문제 해결을 위한 데이터셋으로는 일반 쓰레기, 플라스틱, 종이, 유리 등 10 종류의 쓰레기가 찍힌 사진 데이터셋이 제공됩니다.
여러분에 의해 만들어진 우수한 성능의 모델은 쓰레기장에 설치되어 정확한 분리수거를 돕거나, 어린아이들의 분리수거 교육 등에 사용될 수 있을 것입니다. 부디 지구를 위기로부터 구해주세요! 🌎
<br />

## 📅 Schedule
프로젝트 전체 일정

- 2024.10.02 ~ 2024.10.24

프로젝트 세부 일정

- 2024.10.02 ~ 2024.10.11 : MLFlow 연동
- 2024.10.02 ~ 2024.10.17 : 데이터 EDA 및 Streamlit
- 2024.10.10 ~ 2024.10.24 : Model 실험
- 2024.10.19 ~ 2024.10.21 : Wandb 연동
- 2024.10.20 ~ 2024.10.24 : 모델 앙상블 실험
- 2024.10.20 ~ 2024.10.24 : 모델 평가
<img src="https://github.com/user-attachments/assets/0a1e2d2c-06ba-4ee4-b7a5-620226b9546e" width="500"/>

<br />

## 🥈 Result
- Private 리더보드에서 최종적으로 아래와 같은 결과를 얻었습니다.
<img align="center" src="imgs/result.png" width="600" height="50">

<br />

## 🗃️ Dataset
```
data/
│
├── train.json
├── test.json
│
├── test/
│   ├── 0000.JPG
│   ├── 0001.JPG
│   ├── 0002.JPG
│   ├── ...
│
├── train/
│   ├── 0000.JPG
│   ├── 0001.JPG
│   ├── ... 
```
데이터셋은 검수 및 정제된 ImageNet Skech 데이터셋으로 이미지 수량이 많은 상위 500개의 객체로 이뤄져 있으며, 데이터는 다음과 같이 요약됩니다.
- 각 클래스에 따라 파충류, 개 등 유사한 클래스가 다수 포함되어 있습니다.

	| ![n01729322](https://github.com/user-attachments/assets/1a30b986-8b15-439b-97b5-c1f79f9f3579) | ![n01735189](https://github.com/user-attachments/assets/bcba02eb-384d-47bf-b992-f21f2e95746c) |
	| :---: | :---: |
	| n01729322 (target 32) | n01735189 (target 33) |



- 각 클래스 당 29~31개의 이미지를 가지고 있습니다.

  <img src="https://github.com/user-attachments/assets/57b6af62-329c-4401-89ad-22c8e534f42d" width="500"/>

- 이미지의 크기는 다양하며, 밑의 그래프를 따릅니다.

  <img src="https://github.com/user-attachments/assets/d4a88a8e-b85c-46fb-8f65-ce46f994fa1c" width="500"/>

- 학습데이터는 15,021개이며, 평가데이터는 10,014개입니다.
<br />

## ⚙️ Requirements

### env.
이 프로젝트는 Ubuntu 20.04.6 LTS, CUDA Version: 12.2, Tesla v100 32GB의 환경에서 훈련 및 테스트되었습니다.

### Installment
또한, 이 프로젝트에는 다앙한 라이브러리가 필요합니다. 다음 단계를 따라 필요한 모든 의존성을 설치할 수 있습니다.
``` bash
  git clone https://github.com/boostcampaitech7/level2-imageclassification-cv-23.git
  pip install -r requirements.txt
```

<br />

## 🎉 Project

### 1. Structure
  ```bas
project
├── data
│   ├── augmentation.py
│   ├── dataset.py
│   ├── DDHS_muti.ipynb
│   ├── __init__.py
│   └── readme.md
├── ensemble_inference.py
├── ensemble.sh
├── evaluation.py
├── evaluation.sh
├── imgs
│   └── result.png
├── inference.py
├── inference.sh
├── model
│   ├── __init__.py
│   ├── model.py
│   └── readme.md
├── README.md
├── src
│   ├── early_stopping.py
│   ├── __init__.py
│   ├── loss.py
│   ├── loss_visualization.py
│   └── readme.md
├── sweep_config.yaml
├── sweep_run.sh
├── train.py
├── train.sh
├── utils
│   ├── ensemble_and_evaluation.py
│   ├── __init__.py
│   └── utils.py
├── wandb_ex.md
└── wandb_train.py
  ```

### 2. train
- 모델 훈련을 위해 다음을 실행하세요
  ```bash
  bash train.sh
  ```
- 하이퍼파라미터 및 인자 설명

  - **lrs**: 모델 학습 시 가중치 업데이트의 크기를 결정합니다.

  - **batch_size**: 한 번에 처리할 데이터 샘플의 수을 결정합니다.

  - **epochs**: 전체 데이터셋을 몇 번 반복하여 학습할 것인지를 결정합니다.

  - **gamma**: 학습률 스케줄링에서 사용되는 감쇠 비율을 결정합니다.

  - **lr_decay**: 학습률 감소 주기를 결정합니다.

  - **L1 및 L2**: L1, L2 규제를 위한 하이퍼파라미터를 결정합니다.

  - **early_stopping_delta**: Early Stopping를 판단을 위한 허용 오차 결정합니다.

  - **early_stopping_patience**: 성능 향상이 없을 때 기다리는 에폭 수 결정합니다.

  - **cross_validation_expression**: cross_validationd을 위한 명시적 변수입니다. (Cross validation을 원치 않을 때는 flag를 지우면 됩니다.)

  - **AMP**: 학습 속도를 위한 자동 혼합 정밀도 (Automatic Mixed Precision)의 명시적 변수입니다. (FP16으로 설정되며, AMP을 원치 않을 때는 flag를 지우면 됩니다.)

  - **scheduler_type**: 사용하고자 하는 학습률 스케줄러의 종류를 cosine으로 결정합니다. (이 flag가 없으면 StepLR이 됩니다.)

  - **min_lr**: CosineAnnealingWarmRestarts 스케줄러에서 사용할 최소값의 learning rate를 설정합니다. 

  - **epochs_per_restart**: 첫번째 restart를 위한 iteration(T_0)을 계산하기 위해 학습 과정 중 재시작을 허용할 epoch 주기를 설정합니다. 

  - **models_and_img_sizes**: 사용할 모델과 입력 이미지의 크기를 지정합니다. (모델 이름과 이미지 크기는 띄어쓰기로 구분됩니다.)

  - **train_csv_file**: 학습에 사용할 데이터의 경로를 결정합니다.

  - **traindata_info_file**: 학습 데이터에 대한 추가 정보를 담고 있는 파일의 경로입니다.

  - **save_result_path**: 학습 결과 및 모델을 저장할 경로입니다.

### 3. Inference
- 모델 추론을 위해 다음을 실행하세요
  ```bash
  bash inference.sh
  ```
- 하이퍼파라미터 및 인자 설명
  - train.sh와 동일하지만, 모델과 이미지 크기를 나눠서 받습니다.
  - **model_name**: 추론에 사용할 모델의 이름입니다.

  - **img_size**: 입력 이미지의 크기를 정의합니다.

  - **testdata_dir**: 테스트에 사용할 데이터의 경로를 지정합니다.

  - **testdata_info_file**: 테스트 데이터에 대한 추가 정보를 담고 있는 파일의 경로를 지정합니다.

  - **save_result_path**: 추론 결과를 저장할 경로를 지정합니다.

### 4. ensemble
- 앙상블 학습을 위해 다음을 실행하세요
  ```bash
  bash ensemble.sh
  ```
- 하이퍼파라미터 및 인자 설명
  - **model_n_img_size**: 사용할 모델들과 이미지 크기를 정의합니다. 형식: `"모델이름,모델타입,이미지크기;..."`입니다.
  - 외에 train.sh 및 inference.sh와 동일합니다.

### 5. evaluation
- 모델의 성능 평가를 위해 class별 recall을 반환하고 시각화합니다.
- 모델의 평가를 위해 다음을 실행하세요
  ```bash
  bash evaluation.sh
  ```
- 하이퍼파라미터 및 인자 설명
  - **worst_n**: 가장 recall이 낮은 n개의 class를 반환하도록 개수를 지정합니다. (Default=10)
  - **evaldata_dir**: 평가에 사용할 데이터의 경로를 지정합니다. 평가 시에는 true값과의 비교가 필요하므로 label이 포함된 data를 선택합니다.

  - **evaldata_info_file**: 평가 데이터에 대한 추가 정보를 담고 있는 파일의 경로를 지정합니다.
  - 외에 ensemble.sh와 동일합니다.

<br />

## 🧑‍🤝‍🧑 Contributors
<div align="center">
<table>
  <tr>
    <td align="center"><a href="https://github.com/Yeon-ksy"><img src="https://avatars.githubusercontent.com/u/124290227?v=4" width="100px;" alt=""/><br /><sub><b>김세연</b></sub><br />
    </td>
        <td align="center"><a href="https://github.com/jihyun-0611"><img src="https://avatars.githubusercontent.com/u/78160653?v=4" width="100px;" alt=""/><br /><sub><b>안지현</b></sub><br />
    </td>
        <td align="center"><a href="https://github.com/dhfpswlqkd"><img src="https://avatars.githubusercontent.com/u/123869205?v=4" width="100px;" alt=""/><br /><sub><b>김상유</b></sub><br />
    </td>
        <td align="center"><a href="https://github.com/K-ple"><img src="https://avatars.githubusercontent.com/u/140207345?v=4" width="100px;" alt=""/><br /><sub><b>김태욱</b></sub><br />
    </td>
        <td align="center"><a href="https://github.com/myooooon"><img src="https://avatars.githubusercontent.com/u/168439685?v=4" width="100px;" alt=""/><br /><sub><b>김윤서</b></sub><br />
    </td>
  </tr>
</table>
</div>

## ⚡️ Detail   
- 프로젝트에 대한 자세한 내용은 [Wrap-Up Report](https://github.com/boostcampaitech7/level1-imageclassification-cv-23/blob/b21747b156fd301b04d122964c8d4433777f75b7/utils/CV%EA%B8%B0%EC%B4%88%EB%8C%80%ED%9A%8C_CV_%ED%8C%80%20%EB%A6%AC%ED%8F%AC%ED%8A%B8(23%EC%A1%B0).pdf) 에서 확인할 수 있습니다.
