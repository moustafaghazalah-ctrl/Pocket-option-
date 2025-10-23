import streamlit as st
import pandas as pd
import numpy as np
import os
from datetime import datetime
from sklearn.preprocessing import StandardScaler
import matplotlib.pyplot as plt


# =========================
# إعدادات قابلة للتعديل
# =========================
MODEL_PATH = 'lstm_otc_model.h5' # ضع ملف النموذج هنا إن كان متوفراً
SCALER_PATH = 'scaler.npy' # ملف المخزن للـ scaler (اختياري)
WINDOW = 60
FEATURES = ["open","high","low","close","volume","rsi14","ema12"]
THRESHOLD = 0.6
ASSET = "OTC_ASSET_SYMBOL" # ضع هنا رمز الأصل كما يظهر في Pocket Option (مثلاً 'EURUSD')
TIMEFRAME = "1m"


# =========================
# محاولة استيراد عميل Pocket Option (مكتبة المجتمع)
# =========================
PO_AVAILABLE = True
try:
from pocketoptionapi.stable_api import PocketOption
except Exception:
PO_AVAILABLE = False


