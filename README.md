/ # Butterworth low pass filter

``` python

from scipy import signal

def Filter_Low(Var1, Fl, Nf, SamplingRate):
    '''
    Filter setting
    Fl: ローパスフィルターの遮断周波数 (Hz)
    Nf: 4 フィルタの次数
    SamplingRate:  測定機器の遮断周波数 (Hz)
    '''

    bl, al = signal.butter(Nf, Fl, 'low', fs = SamplingRate)
    FilterData = signal.filtfilt(bl, al, Var1).flatten()
    
    LowpassFilterData = pd.Series(FilterData)

    return LowpassFilterData
```



``` python

import pandas as pd
import scipy.signal

def BandpathFilter(Var, LOW, HIGH, SamplingRate):
    '''
    Filter setting
    LOW: 低周波数域
    HIGH: 高周波数域
    SamplingRate:　測定機器の遮断周波数
    '''

    fs = SamplingRate
    lowcut = LOW
    highcut = HIGH

    nyq = 0.5 * fs
    low = lowcut / nyq
    high = highcut / nyq

    order = 2

    b, a = scipy.signal.butter(order, [low, high], 'bandpass', analog=False)
    FilterData = scipy.signal.filtfilt(b, a, Var, axis=0).flatten()
    
    BandpathFilterData = pd.Series(FilterData)
    
    return BandpathFilterData
```
