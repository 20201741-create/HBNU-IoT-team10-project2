# Federated Blood Supply Chain Demand Forecasting: 연합학습을 이용한 혈액 공급망 수요 예측

연합 학습을 이용한 혈액 공급망 수요 예측 연구용 시뮬레이션 코드 저장소입니다. 이 저장소는 KDD 2023 워크숍 논문 [Federated Blood Supply Chain Demand Forecasting: A Case Study](https://openreview.net/forum?id=2c0hdQDvf5g)의 시뮬레이션 및 재현을 위해 제공됩니다.

## 개요 및 실행/설치 매뉴얼(macOS를 기준으로 작성되었습니다.)

이 저장소는 시뮬레이션 데이터 생성(`arima` 폴더), 연합 학습 시뮬레이션(`flower` 폴더), 평가 및 시각화 도구를 포함합니다. 연합 학습 프레임워크로는 PyTorch 기반의 `Flower`를 사용하며, baseline 모델로는 `LSTM`을 사용합니다.

### 설치 환경

- 사전 요구사항: `conda` 설치 (또는 호환 가능한 Python 환경)
- 의존성 설치 및 conda 환경 생성은 제공된 스크립트 `install.sh`로 자동화되어 있습니다.
- 다만, 2025년 12월 기준 호환되지 않는 환경이 있기에 아나콘다 설치를 권장합니다.

```bash
git clone https://github.com/denoslab/fl-blood-supply-chain.git
cd fl-blood-supply-chain

source install.sh
pip install -U "flwr[simulation]"
pip install --upgrade kaleido

mkdir -p flower/savedmodels
mkdir -p flower/evaluation

conda install "pandas<2.0.0"

# Pandas 다운그레이드
```

> 참고: 시스템에 따라 `bash` 대신 `zsh`에서 `source` 사용이 필요할 수 있습니다.

> install.sh에 해당 설치 환경을 위한 명령어 추가를 권장합니다.

### 실행 환경

```bash
conda activate flower

python arima/generate_case_balanced_iid.py
python arima/generate_case_imbalanced_iid.py
python arima/generate_case_random_zeros.py
python arima/generate_heterogenous_add.py
python arima/generate_heterogenous_concat.py

# 생성하고 싶은 시뮬레이션 환경 명령어 입력

source run.sh

# 생성된 데이터는 기본적으로 arima에 저장됩니다.
```

> 참고: generate_heterogenous 환경의 경우 생성된 시뮬레이션 데이터의 이름을 C#.csv의 형태로 변경해 주어야 합니다.

## 결과

- 시뮬레이션 완료 후 결과는 `flower/evaluation` 디렉터리에 PDF 및 HTML 형태로 저장됩니다.
- 대시보드: `flower/evaluation/DASHBOARD.html` 을 열어 시각화된 결과를 확인하세요.
- 학습된 모델은 `flower/saved_models` 에 저장됩니다.

## 프로젝트 수행 내용

- 데이터 예측 모델 GRU 추가 후 실행
- 연합학습 알고리즘 개선 시도
- 하이퍼파라미터 변경 후 구현체 실행

## Reference

Maryam Motamedi, Na Li, Douglas G Down, and Nancy M Heddle. 2021. Demand forecasting for platelet usage: from univariate time series to multivariate models. [arXiv preprint arXiv:2101.02305](https://arxiv.org/abs/2101.02305) (2021)

## Citation

```
@inproceedings{wei2023federated,
  title={Federated Blood Supply Chain Demand Forecasting: A Case Study},
  author={Wei, Hanzhe and Li, Na and Wu, Jiajun and Zhou, Jiayu and Drew, Steve},
  booktitle={International Workshop on Federated Learning for Distributed Data Mining},
  year={2023}
}
```
