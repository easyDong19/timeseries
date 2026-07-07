# Time Series Analysis (시계열 분석)

ARIMA / SARIMA 계열 모형을 이용해 시계열 데이터의 **정상성(stationarity)을 진단하고, 모형을 식별·추정한 뒤 예측(forecasting)** 을 수행한 분석 프로젝트입니다. 시계열 분석 수업 과제와 팀 프로젝트 자료를 하나의 저장소에 정리했습니다.

## 작업 기간

- **커밋 기준: 2023-11-24** (`eb08d5d` — "sarima 분석 완료")
- Git 이력상 전체 작업 결과물이 한 번의 커밋으로 스냅샷되어 있어, 저장소 이력만으로 정확한 착수일은 특정하기 어렵습니다. 커밋 메시지와 노트북 구성으로 볼 때 2023년 하반기(가을학기) 시계열 분석 학습·과제 기간에 진행된 작업입니다.

## 무엇을 했는지

세 개의 Jupyter 노트북에서 시계열 분석의 전 과정을 실습·적용했습니다.

### 1. `pes.ipynb` — PES 분기 데이터 스프레드 분석
- 데이터: `TAF_2_Stationary_Time_Series_PES_quarterly.xls` (분기별 시계열)
- **정상성 검정**: ADF test / KPSS test로 원계열과 차분 계열의 정상성 비교 (귀무가설 해석 포함)
- **모형 식별**: ACF / PACF 시각화
- **모형 비교**: `ARIMA(7,0,0)`(Model 1)과 `ARIMA(2,0,[1,7])`(Model 2)를 innovations MLE로 추정
- **예측 성능 평가**: one-step-ahead 예측을 반복 수행하고 두 모형의 **MSPE(평균제곱예측오차)** 비교
- **유의성 검정**: OLS 기반 Joint F-test로 계수 유의성 확인

### 2. `assignment/ARIMA.ipynb` — 과제: AirPassengers ARIMA/SARIMA
- 데이터: `AirPassengers.csv` (월별 항공 승객 수, 대표적 계절성 시계열)
- ADF / KPSS 검정으로 비정상성 확인 → ACF / PACF 분석
- `ARIMA` 및 `SARIMAX`를 이용한 계절성 시계열 모형화

### 3. `dm_team/predict_bgr.ipynb` — 팀 프로젝트: SARIMA 이익 예측
- 데이터: `profit_bgr.xlsx` (기업 이익 시계열, 분기 주기)
- **계절 차분** 후 여러 `SARIMAX` 후보 모형(`(0,0,1)`, `(1,0,1)`, `(1,0,1)x(1,0,1,4)` 등) 비교
- `pmdarima.auto_arima`로 최적 차수·주기 자동 탐색
- 최종 `SARIMAX(0,1,1)x(0,1,0,4)` 모형으로 향후 5기간 예측, **MAPE** 로 예측 정확도 평가

## 프로젝트 성격

- **분야**: 시계열 분석 / 예측 (Time Series Forecasting)
- **성격**: 학습·과제 및 팀 프로젝트용 분석 노트북 모음
- **핵심 기법**: ADF·KPSS 정상성 검정, ACF/PACF 기반 모형 식별, ARIMA / SARIMA(SARIMAX) 추정, one-step-ahead 예측, MSPE·MAPE 예측 평가, auto_arima 자동 차수 선택

## 기술 스택

- **Python** (Jupyter Notebook / DataSpell)
- **statsmodels** — `ARIMA`, `SARIMAX`, `adfuller`, `kpss`, `acf`, `plot_acf/pacf`, `OLS`
- **pmdarima** — `auto_arima`
- **pandas / numpy** — 데이터 처리
- **matplotlib** — 시각화

## 저장소 구성

```
timeseries/
├── pes.ipynb                                        # PES 분기 스프레드 ARIMA 분석
├── TAF_2_Stationary_Time_Series_PES_quarterly.xls   # PES 분기 데이터
├── assignment/
│   ├── ARIMA.ipynb                                  # 과제: AirPassengers ARIMA/SARIMA
│   └── AirPassengers.csv                            # 월별 항공 승객 수 데이터
└── dm_team/
    ├── predict_bgr.ipynb                            # 팀 프로젝트: SARIMA 이익 예측
    └── profit_bgr.xlsx                              # 기업 이익 시계열 데이터
```

## 실행 방법

```bash
pip install pandas numpy matplotlib statsmodels pmdarima openpyxl xlrd
jupyter notebook
```

> 참고: 노트북 내 데이터 경로가 `/Users/easydong/DataspellProjects/timeseries/...` 절대경로로 하드코딩되어 있어, 다른 환경에서 실행하려면 `read_excel` / `read_csv` 경로를 저장소 기준 상대경로로 수정해야 합니다.
