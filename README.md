# Signal-Filter

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
    
    Rs = pd.Series(FilterData)
    
    return Rs
```
