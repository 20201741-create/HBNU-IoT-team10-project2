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

conda install "pandas<2.0.0”
```

> 참고: 시스템에 따라 `bash` 대신 `zsh`에서 `source` 사용이 필요할 수 있습니다.

## Usage

1. 적절한 conda 환경을 활성화하세요(위 `install.sh`가 환경을 생성한 경우 해당 환경을 활성화).

2. 시뮬레이션용 데이터 생성:
- `arima` 폴더에는 클라이언트별 시뮬레이션 데이터를 생성하는 스크립트들이 있습니다. 예를 들어 균형된 IID 케이스 데이터를 생성하려면:

```bash
git clone https://github.com/denoslab/fl-blood-supply-chain.git
cd fl-blood-supply-chain
conda activate flower
python arima/generate_case_balanced_iid.py
mkdir -p flower/savemodels
mkdir -p flower/evaluation
source run.sh

# 생성된 데이터는 기본적으로 arima/data 디렉터리에 저장됩니다.
```

3. 중앙집중식 기준선 및 연합 학습 실행:
- 루트 폴더의 `run.sh` 스크립트는 중앙집중식 학습과 연합 학습 시뮬레이션(클라이언트 로컬 학습 포함)을 자동으로 실행합니다.

```bash
source run.sh
```

- 또는 직접 실행하려면 `flower/central.py`(중앙집중식 LSTM baseline) 및 `flower/fl_simulation.py`(연합 학습 시뮬레이션)를 참고하세요.

4. 평가 및 결과 보기:
- 시뮬레이션 완료 후 결과는 `flower/evaluation` 디렉터리에 PDF 및 HTML 형태로 저장됩니다.

## Results

- 대시보드: `flower/evaluation/DASHBOARD.html` 을 열어 시각화된 결과를 확인하세요.
- 학습된 모델은 `flower/saved_models` 에 저장됩니다.

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
