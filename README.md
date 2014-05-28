MapSatAltitude
==============

This is a command-line tool, written in Octave/Matlab, to answer the question:
	"What orbit should I use to most efficiently scan `some planetary body`
	with `some supported scanner` given that only want to use one vessel?"


Supported Scanners
==================

Scanners are defined in scanners.txt. This is a simple, tab-delimited table containing
information needed to make the calculation and some information to make the output prettier.

When running `MapSatAltitude.m`, the response to `Scanner name?` should be the first column of one
of these rows:

```
Name	FOV	HalfFOV	AltitudeMin	AltitudeIdeal	AltitudeMax	LongName
RADAR	5.00	2.50	5000.00		5000.00		500000.00	SCAN RADAR Altimetry Sensor
Multi	4.00	2.00	5000.00		250000.00	500000.00	SCAN Multispectral Sensor
SAR	2.00	1.00	5000.00		750000.00	800000.00	SCAN SAR Altimetry Sensor
KSmall	2.20	1.10	250000.00	250000.00	250000.00	KE-S210 Compact Survey Unit
KMedium	2.20	1.10	1200000.00	1200000.00	1200000.00	KE-S110 Medium Survey Unit
```

Supported Planets
==================

Planets are defined in `PlanetInfos.txt`. This has the same format as the scanners file, with different fields.

```
Name	Radius		Day		GM			SOI		Atmo
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Earth	6371000.00	86400.002	398600441800000.000	923795000.000	180000.000
Moon	1737100.00	2360584.685	4902800000000.000	66009800.000	0.000
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%% Original Planets from here down ...
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Kerbol	26160000.00	432000.000	1172332800000000000.000	999999999999.00	0.000
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Moho	250000.00	1210000.000	168609378654.509	9646663.000	0.000
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Eve	700000.00	80500.000	8171730229210.87	85109365.000	96000.000
Gilly	13000.00	28255.000	8289449.81471		126123.270	0.000
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Kerbin	600000.00	21600.000	3531600000000.000	84159286.000	69078.000
Mun	200000.00	138984.380	65138397520.7807	2429559.100	0.000
Minmus	60000.00	40400.000	1765800026.31247	2247428.400	0.000
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Duna	320000.00	65517.859	301363211975.098	47921949.000	41446.000
Ike	130000.00	65517.862	18568368573.144		1049598.900	0.000
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Dres	138000.00	34800.000	21484488600.000		32832840.000	0.000
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Jool	6000000.00	36000.00	282528004209995.000	2455985185.000	200000.00
Laythe	500000.00	52980.879	1962000029236.08	3723645.800	50000.000
Vall	300000.00	105962.090	207481499473.751	2406401.400	0.000
Tylo	600000.00	211926.360	2825280042099.95	10856518.000	0.000
Bop	65000.00	544507.400	2486834944.41491	1221061.000	0.000
Pol	44000.00	901902.620	721702080.000		1042138.900	0.000
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Eeloo	210000.00	19460.000	74410814527.0496	119082942.000	0.000
```

Example Session
==============

```
Planet:     Mun
Radius:     200 km
Sync.Orbit: 2970.56 km
SOI:        2429.56 km
Day Length: 38h 36m 24s

Scan line resolution: 200
Field of view: 2.000000 deg
Sidelap range: 1.000000 - 1.250000
Altitude Range: 5.0 km - 800.0 km in 15.9 m steps (50001 possible zones)
Minimum altitude chosen because:
	[SCAN SAR Altimetry Sensor] has a minimum range of 5.0 km

Maximum Altitude chosen because:
	[SCAN SAR Altimetry Sensor] has a maximum range of 800.00 km


 Number of Zones: 79

---------------------------
Mun, Sidelap 1 - 1.25:
                      SMA         Altitude         Inclination Orbital   Time to Scan        Eff.   Swath    Resolution
Zone  Res  Sidelap             Ideal      +/- Range    (deg)   Period   Ideal       diff      FOV     Width   (deg)   (km) 
========================================================================================================

  1  229/439  (1.03)  390.807 km  190.807  +/-  0.02 km  87.52   1h 40.2m   366h 43.3m +01.3m  0.88   0.8  0.0042  14.68 m
  2  227/435  (1.04)  393.256 km  193.256  +/-  0.02 km  87.50   1h 41.2m   366h 46.8m +01.3m  0.89   0.9  0.0043  15.05 m
  3  177/338  (1.00)  414.896 km  214.896  +/-  0.10 km  87.29   1h 49.6m   308h 48.1m +06.4m  0.99   1.1  0.0053  18.62 m
  4  188/359  (1.06)  414.991 km  214.991  +/-  0.06 km  87.29   1h 49.7m   328h 07.2m +04.5m  0.99   1.1  0.0053  18.63 m
  5  199/380  (1.13)  415.071 km  215.071  +/-  0.06 km  87.29   1h 49.7m   347h 24.8m +04.8m  0.99   1.1  0.0053  18.65 m
  6  210/401  (1.19)  415.150 km  215.150  +/-  0.06 km  87.28   1h 49.7m   366h 43.0m +05.1m  0.99   1.1  0.0053  18.66 m
  7  208/397  (1.21)  417.949 km  217.949  +/-  0.05 km  87.26   1h 50.9m   366h 44.2m +03.8m  1.01   1.1  0.0055  19.15 m
  8  197/376  (1.15)  418.012 km  218.012  +/-  0.06 km  87.26   1h 50.9m   347h 25.0m +04.8m  1.01   1.1  0.0055  19.16 m
  9  186/355  (1.08)  418.108 km  218.108  +/-  0.08 km  87.26   1h 50.9m   328h 06.4m +05.6m  1.01   1.1  0.0055  19.18 m
 10  175/334  (1.02)  418.203 km  218.203  +/-  0.10 km  87.25   1h 50.9m   308h 48.2m +06.3m  1.01   1.1  0.0055  19.19 m
 11  141/268  (1.02)  443.071 km  243.071  +/-  0.14 km  87.01   2h 01.0m   270h 10.9m +07.9m  1.12   1.4  0.0068  23.82 m
 12  151/287  (1.09)  443.214 km  243.214  +/-  0.11 km  87.00   2h 01.0m   289h 29.5m +06.5m  1.12   1.4  0.0068  23.85 m
 13  161/306  (1.16)  443.341 km  243.341  +/-  0.11 km  87.00   2h 01.1m   308h 47.4m +07.0m  1.12   1.4  0.0068  23.87 m
 14  171/325  (1.24)  443.452 km  243.452  +/-  0.10 km  87.00   2h 01.1m   328h 06.3m +06.4m  1.12   1.4  0.0068  23.89 m
 15  159/302  (1.18)  447.252 km  247.252  +/-  0.11 km  86.96   2h 02.7m   308h 47.8m +06.9m  1.14   1.4  0.0071  24.64 m
 16  149/283  (1.11)  447.380 km  247.380  +/-  0.13 km  86.96   2h 02.8m   289h 29.5m +07.4m  1.14   1.4  0.0071  24.67 m
 17  139/264  (1.04)  447.539 km  247.539  +/-  0.14 km  86.96   2h 02.8m   270h 11.2m +07.8m  1.14   1.4  0.0071  24.70 m
 18  124/235  (1.02)  460.306 km  260.306  +/-  0.19 km  86.83   2h 08.1m   250h 51.6m +09.4m  1.20   1.6  0.0078  27.32 m
 19  143/271  (1.18)  460.465 km  260.465  +/-  0.10 km  86.83   2h 08.2m   289h 29.1m +05.4m  1.20   1.6  0.0078  27.35 m
 20  142/269  (1.19)  462.787 km  262.787  +/-  0.10 km  86.80   2h 09.2m   289h 31.5m +05.4m  1.21   1.6  0.0080  27.84 m
 21  123/233  (1.03)  462.946 km  262.946  +/-  0.19 km  86.80   2h 09.2m   250h 52.1m +09.3m  1.21   1.6  0.0080  27.87 m
 22  109/206  (1.01)  476.445 km  276.445  +/-  0.24 km  86.66   2h 14.9m   231h 32.9m +10.4m  1.28   1.8  0.0088  30.81 m
 23  118/223  (1.09)  476.683 km  276.683  +/-  0.21 km  86.66   2h 15.0m   250h 51.4m +09.8m  1.28   1.8  0.0088  30.86 m
 24  127/240  (1.18)  476.890 km  276.890  +/-  0.17 km  86.66   2h 15.1m   270h 10.2m +08.9m  1.28   1.8  0.0089  30.91 m
 25  125/236  (1.21)  482.264 km  282.264  +/-  0.19 km  86.60   2h 17.4m   270h 10.3m +09.6m  1.30   1.8  0.0092  32.12 m
 26  116/219  (1.12)  482.487 km  282.487  +/-  0.21 km  86.60   2h 17.5m   250h 52.3m +09.7m  1.30   1.8  0.0092  32.17 m
 27  107/202  (1.04)  482.725 km  282.725  +/-  0.24 km  86.59   2h 17.6m   231h 33.4m +10.3m  1.31   1.8  0.0092  32.22 m
 28  113/213  (1.16)  491.407 km  291.407  +/-  0.08 km  86.50   2h 21.3m   250h 50.7m +03.7m  1.35   2.0  0.0098  34.23 m
 29   94/177  (1.00)  497.433 km  297.433  +/-  0.32 km  86.44   2h 23.9m   212h 13.5m +12.2m  1.37   2.0  0.0102  35.67 m
 30  111/209  (1.19)  497.735 km  297.735  +/-  0.24 km  86.43   2h 24.0m   250h 50.7m +10.8m  1.38   2.0  0.0102  35.74 m
 31  110/207  (1.20)  500.947 km  300.947  +/-  0.22 km  86.40   2h 25.4m   250h 52.0m +10.0m  1.39   2.1  0.0105  36.51 m
 32   93/175  (1.02)  501.249 km  301.249  +/-  0.35 km  86.40   2h 25.5m   212h 14.2m +13.3m  1.39   2.1  0.0105  36.59 m
 33   92/173  (1.03)  505.065 km  305.065  +/-  0.35 km  86.35   2h 27.2m   212h 12.7m +13.2m  1.41   2.1  0.0107  37.52 m
 34  108/203  (1.23)  507.545 km  307.545  +/-  0.19 km  86.33   2h 28.3m   250h 54.5m +08.5m  1.42   2.2  0.0109  38.13 m
 35   91/171  (1.05)  508.881 km  308.881  +/-  0.14 km  86.31   2h 28.9m   212h 12.1m +05.4m  1.43   2.2  0.0110  38.46 m
 36   89/167  (1.08)  517.117 km  317.117  +/-  0.37 km  86.22   2h 32.5m   212h 13.3m +13.5m  1.46   2.3  0.0116  40.54 m
 37   97/182  (1.18)  517.467 km  317.467  +/-  0.30 km  86.22   2h 32.7m   231h 32.3m +12.2m  1.47   2.3  0.0116  40.63 m
 38   95/178  (1.21)  525.194 km  325.194  +/-  0.32 km  86.13   2h 36.1m   231h 32.6m +12.6m  1.50   2.4  0.0122  42.64 m
 39   87/163  (1.11)  525.560 km  325.560  +/-  0.37 km  86.13   2h 36.2m   212h 14.0m +13.3m  1.50   2.4  0.0122  42.73 m
 40   79/148  (1.01)  525.989 km  325.989  +/-  0.46 km  86.13   2h 36.4m   192h 54.7m +15.2m  1.51   2.5  0.0123  42.85 m
 41   85/159  (1.14)  534.400 km  334.400  +/-  0.32 km  86.03   2h 40.2m   212h 17.5m +11.4m  1.54   2.6  0.0129  45.09 m
 42   77/144  (1.04)  535.640 km  335.640  +/-  0.49 km  86.02   2h 40.7m   192h 52.9m +16.0m  1.55   2.6  0.0130  45.42 m
 43   84/157  (1.16)  538.884 km  338.884  +/-  0.40 km  85.98   2h 42.2m   212h 14.2m +14.1m  1.57   2.7  0.0133  46.30 m
 44   83/155  (1.17)  543.447 km  343.447  +/-  0.41 km  85.93   2h 44.3m   212h 12.1m +14.5m  1.59   2.7  0.0136  47.56 m
 45   82/153  (1.19)  548.217 km  348.217  +/-  0.41 km  85.88   2h 46.5m   212h 13.7m +14.4m  1.61   2.8  0.0140  48.89 m
 46   81/151  (1.21)  553.003 km  353.003  +/-  0.43 km  85.82   2h 48.6m   212h 11.7m +14.8m  1.63   2.9  0.0144  50.24 m
 47   73/136  (1.11)  556.517 km  356.517  +/-  0.54 km  85.78   2h 50.2m   192h 55.0m +16.9m  1.65   2.9  0.0147  51.25 m
 48   80/149  (1.22)  557.932 km  357.932  +/-  0.46 km  85.77   2h 50.9m   212h 10.9m +15.8m  1.65   3.0  0.0148  51.66 m
 49   65/121  (1.01)  560.731 km  360.731  +/-  0.51 km  85.73   2h 52.2m   173h 36.0m +14.2m  1.67   3.0  0.0150  52.47 m
 50   79/147  (1.24)  563.004 km  363.004  +/-  0.00 km  85.71   2h 53.3m   212h 19.9m +00.0m  1.68   3.0  0.0152  53.13 m
 51   64/119  (1.03)  567.011 km  367.011  +/-  0.68 km  85.66   2h 55.0m   173h 33.9m +18.9m  1.70   3.1  0.0156  54.31 m
 52   71/132  (1.14)  567.647 km  367.647  +/-  0.56 km  85.66   2h 55.3m   192h 52.9m +17.0m  1.70   3.1  0.0156  54.50 m
 53   69/128  (1.18)  579.445 km  379.445  +/-  0.59 km  85.52   3h 00.8m   192h 53.6m +17.6m  1.75   3.3  0.0166  58.06 m
 54   62/115  (1.06)  580.113 km  380.113  +/-  0.73 km  85.51   3h 01.1m   173h 34.4m +19.7m  1.76   3.3  0.0167  58.26 m
 55   61/113  (1.08)  586.934 km  386.934  +/-  0.59 km  85.43   3h 04.4m   173h 36.1m +15.7m  1.79   3.5  0.0173  60.37 m
 56   67/124  (1.22)  591.768 km  391.767  +/-  0.64 km  85.37   3h 06.6m   192h 51.2m +18.7m  1.81   3.5  0.0177  61.89 m
 57   59/109  (1.12)  601.149 km  401.149  +/-  0.81 km  85.26   3h 11.0m   173h 31.9m +21.1m  1.85   3.7  0.0186  64.90 m
 58   58/107  (1.14)  608.717 km  408.717  +/-  0.84 km  85.17   3h 14.7m   173h 34.2m +21.6m  1.89   3.9  0.0193  67.37 m
 59   51/94   (1.03)  613.344 km  413.344  +/-  1.11 km  85.12   3h 16.8m   154h 10.7m +25.2m  1.91   3.9  0.0197  68.90 m
 60   56/103  (1.19)  624.315 km  424.315  +/-  0.70 km  84.99   3h 22.2m   173h 35.0m +17.5m  1.96   4.2  0.0208  72.61 m
 61   49/90   (1.07)  631.470 km  431.470  +/-  1.16 km  84.90   3h 25.6m   154h 12.2m +25.5m  1.99   4.3  0.0215  75.09 m
 62   55/101  (1.21)  632.519 km  432.519  +/-  0.91 km  84.89   3h 26.2m   173h 32.1m +22.4m  2.00   4.3  0.0216  75.45 m
 63   47/86   (1.12)  650.963 km  450.963  +/-  1.24 km  84.66   3h 35.2m   154h 13.2m +26.5m  2.08   4.7  0.0235  82.03 m
 64   40/73   (1.01)  664.256 km  464.256  +/-  1.37 km  84.50   3h 41.8m   134h 55.3m +25.0m  2.14   5.0  0.0249  86.95 m
 65   45/82   (1.17)  672.062 km  472.062  +/-  1.40 km  84.40   3h 45.7m   154h 14.0m +28.9m  2.18   5.2  0.0258  89.90 m
 66   39/71   (1.03)  676.594 km  476.594  +/-  1.70 km  84.34   3h 47.9m   134h 51.0m +30.6m  2.20   5.3  0.0263  91.64 m
 67   38/69   (1.06)  689.696 km  489.696  +/-  1.72 km  84.18   3h 54.6m   134h 52.9m +30.3m  2.26   5.5  0.0277  96.75 m
 68   43/78   (1.22)  694.577 km  494.577  +/-  1.51 km  84.11   3h 57.1m   154h 07.8m +30.2m  2.28   5.7  0.0283  98.69 m
 69   37/67   (1.09)  703.306 km  503.306  +/-  1.57 km  84.00   4h 01.6m   134h 53.5m +27.2m  2.32   5.9  0.0293  0.102 km
 70   36/65   (1.11)  717.680 km  517.680  +/-  1.76 km  83.82   4h 09.0m   134h 52.5m +29.9m  2.39   6.2  0.0310  0.108 km
 71   34/61   (1.18)  748.716 km  548.716  +/-  1.72 km  83.41   4h 25.4m   134h 53.5m +27.9m  2.53   7.0  0.0348  0.122 km
 72   29/52   (1.01)  751.451 km  551.451  +/-  1.72 km  83.37   4h 26.8m   115h 37.3m +23.8m  2.55   7.0  0.0352  0.123 km
 73   33/59   (1.21)  765.539 km  565.539  +/-  1.72 km  83.19   4h 34.4m   134h 53.8m +27.3m  2.61   7.4  0.0370  0.129 km
 74   32/57   (1.24)  783.331 km  583.331  +/-  1.65 km  82.95   4h 44.0m   134h 54.4m +25.7m  2.69   7.9  0.0394  0.137 km
 75   25/44   (1.16)  839.982 km  639.982  +/-  1.62 km  82.16   5h 15.4m   115h 39.2m +20.1m  2.96   9.5  0.0474  0.165 km
 76   23/40   (1.24)  895.092 km  695.092  +/-  1.57 km  81.37   5h 47.0m   115h 40.0m +18.3m  3.21  11.2  0.0560  0.195 km
 77   19/33   (1.04)  901.102 km  701.102  +/-  1.56 km  81.29   5h 50.5m    96h 23.5m +15.0m  3.24  11.4  0.0569  0.199 km
 78   18/31   (1.09)  939.453 km  739.453  +/-  1.53 km  80.72   6h 13.2m    96h 24.0m +14.1m  3.42  12.7  0.0634  0.221 km
 79   17/29   (1.10)  982.176 km  782.176  +/-  1.51 km  80.07   6h 38.9m    96h 24.4m +13.4m  3.46  13.6  0.0680  0.238 km
```


The numerator in the 2nd (Res -- Resonance) column is the number of unique equitorial crossings in the total period (Time to Scan column).





Markdown-Formatted Example Output (WITH FOV-dependence)
=======================================================
Zone | UEC | TEC | Sidelap | SMA | Altitude +/- Range | Inclination | Orbital Period | Time to Scan | Eff. FOV | Swath Width | Resolution (deg) | Resolution (km)
 --- | ----| --- | ------- | --- | ------------------ | ----------- | -------------- | ------------ | -------- | ----------- | ---------------- | ---------------
  1 | 229 | 439  | (1.03) |390.807 km |190.807  +/-  0.02 km  |87.52 |  1h 40.2m |  366h 43.3m +01.3m  |0.88 |  0.8 | 0.0042 | 14.68 m
  2 | 227 | 435  | (1.04) |393.256 km |193.256  +/-  0.02 km  |87.50 |  1h 41.2m |  366h 46.8m +01.3m  |0.89 |  0.9 | 0.0043 | 15.05 m
  3 | 177 | 338  | (1.00) |414.896 km |214.896  +/-  0.10 km  |87.29 |  1h 49.6m |  308h 48.1m +06.4m  |0.99 |  1.1 | 0.0053 | 18.62 m
  4 | 188 | 359  | (1.06) |414.991 km |214.991  +/-  0.06 km  |87.29 |  1h 49.7m |  328h 07.2m +04.5m  |0.99 |  1.1 | 0.0053 | 18.63 m
  5 | 199 | 380  | (1.13) |415.071 km |215.071  +/-  0.06 km  |87.29 |  1h 49.7m |  347h 24.8m +04.8m  |0.99 |  1.1 | 0.0053 | 18.65 m
  6 | 210 | 401  | (1.19) |415.150 km |215.150  +/-  0.06 km  |87.28 |  1h 49.7m |  366h 43.0m +05.1m  |0.99 |  1.1 | 0.0053 | 18.66 m
  7 | 208 | 397  | (1.21) |417.949 km |217.949  +/-  0.05 km  |87.26 |  1h 50.9m |  366h 44.2m +03.8m  |1.01 |  1.1 | 0.0055 | 19.15 m
  8 | 197 | 376  | (1.15) |418.012 km |218.012  +/-  0.06 km  |87.26 |  1h 50.9m |  347h 25.0m +04.8m  |1.01 |  1.1 | 0.0055 | 19.16 m
  9 | 186 | 355  | (1.08) |418.108 km |218.108  +/-  0.08 km  |87.26 |  1h 50.9m |  328h 06.4m +05.6m  |1.01 |  1.1 | 0.0055 | 19.18 m
 10 | 175 | 334  | (1.02) |418.203 km |218.203  +/-  0.10 km  |87.25 |  1h 50.9m |  308h 48.2m +06.3m  |1.01 |  1.1 | 0.0055 | 19.19 m
 11 | 141 | 268  | (1.02) |443.071 km |243.071  +/-  0.14 km  |87.01 |  2h 01.0m |  270h 10.9m +07.9m  |1.12 |  1.4 | 0.0068 | 23.82 m
 12 | 151 | 287  | (1.09) |443.214 km |243.214  +/-  0.11 km  |87.00 |  2h 01.0m |  289h 29.5m +06.5m  |1.12 |  1.4 | 0.0068 | 23.85 m
 13 | 161 | 306  | (1.16) |443.341 km |243.341  +/-  0.11 km  |87.00 |  2h 01.1m |  308h 47.4m +07.0m  |1.12 |  1.4 | 0.0068 | 23.87 m
 14 | 171 | 325  | (1.24) |443.452 km |243.452  +/-  0.10 km  |87.00 |  2h 01.1m |  328h 06.3m +06.4m  |1.12 |  1.4 | 0.0068 | 23.89 m
 15 | 159 | 302  | (1.18) |447.252 km |247.252  +/-  0.11 km  |86.96 |  2h 02.7m |  308h 47.8m +06.9m  |1.14 |  1.4 | 0.0071 | 24.64 m
 16 | 149 | 283  | (1.11) |447.380 km |247.380  +/-  0.13 km  |86.96 |  2h 02.8m |  289h 29.5m +07.4m  |1.14 |  1.4 | 0.0071 | 24.67 m
 17 | 139 | 264  | (1.04) |447.539 km |247.539  +/-  0.14 km  |86.96 |  2h 02.8m |  270h 11.2m +07.8m  |1.14 |  1.4 | 0.0071 | 24.70 m
 18 | 124 | 235  | (1.02) |460.306 km |260.306  +/-  0.19 km  |86.83 |  2h 08.1m |  250h 51.6m +09.4m  |1.20 |  1.6 | 0.0078 | 27.32 m
 19 | 143 | 271  | (1.18) |460.465 km |260.465  +/-  0.10 km  |86.83 |  2h 08.2m |  289h 29.1m +05.4m  |1.20 |  1.6 | 0.0078 | 27.35 m
 20 | 142 | 269  | (1.19) |462.787 km |262.787  +/-  0.10 km  |86.80 |  2h 09.2m |  289h 31.5m +05.4m  |1.21 |  1.6 | 0.0080 | 27.84 m
 21 | 123 | 233  | (1.03) |462.946 km |262.946  +/-  0.19 km  |86.80 |  2h 09.2m |  250h 52.1m +09.3m  |1.21 |  1.6 | 0.0080 | 27.87 m
 22 | 109 | 206  | (1.01) |476.445 km |276.445  +/-  0.24 km  |86.66 |  2h 14.9m |  231h 32.9m +10.4m  |1.28 |  1.8 | 0.0088 | 30.81 m
 23 | 118 | 223  | (1.09) |476.683 km |276.683  +/-  0.21 km  |86.66 |  2h 15.0m |  250h 51.4m +09.8m  |1.28 |  1.8 | 0.0088 | 30.86 m
 24 | 127 | 240  | (1.18) |476.890 km |276.890  +/-  0.17 km  |86.66 |  2h 15.1m |  270h 10.2m +08.9m  |1.28 |  1.8 | 0.0089 | 30.91 m
 25 | 125 | 236  | (1.21) |482.264 km |282.264  +/-  0.19 km  |86.60 |  2h 17.4m |  270h 10.3m +09.6m  |1.30 |  1.8 | 0.0092 | 32.12 m
 26 | 116 | 219  | (1.12) |482.487 km |282.487  +/-  0.21 km  |86.60 |  2h 17.5m |  250h 52.3m +09.7m  |1.30 |  1.8 | 0.0092 | 32.17 m
 27 | 107 | 202  | (1.04) |482.725 km |282.725  +/-  0.24 km  |86.59 |  2h 17.6m |  231h 33.4m +10.3m  |1.31 |  1.8 | 0.0092 | 32.22 m
 28 | 113 | 213  | (1.16) |491.407 km |291.407  +/-  0.08 km  |86.50 |  2h 21.3m |  250h 50.7m +03.7m  |1.35 |  2.0 | 0.0098 | 34.23 m
 29 |  94 | 177  | (1.00) |497.433 km |297.433  +/-  0.32 km  |86.44 |  2h 23.9m |  212h 13.5m +12.2m  |1.37 |  2.0 | 0.0102 | 35.67 m
 30 | 111 | 209  | (1.19) |497.735 km |297.735  +/-  0.24 km  |86.43 |  2h 24.0m |  250h 50.7m +10.8m  |1.38 |  2.0 | 0.0102 | 35.74 m
 31 | 110 | 207  | (1.20) |500.947 km |300.947  +/-  0.22 km  |86.40 |  2h 25.4m |  250h 52.0m +10.0m  |1.39 |  2.1 | 0.0105 | 36.51 m
 32 |  93 | 175  | (1.02) |501.249 km |301.249  +/-  0.35 km  |86.40 |  2h 25.5m |  212h 14.2m +13.3m  |1.39 |  2.1 | 0.0105 | 36.59 m
 33 |  92 | 173  | (1.03) |505.065 km |305.065  +/-  0.35 km  |86.35 |  2h 27.2m |  212h 12.7m +13.2m  |1.41 |  2.1 | 0.0107 | 37.52 m
 34 | 108 | 203  | (1.23) |507.545 km |307.545  +/-  0.19 km  |86.33 |  2h 28.3m |  250h 54.5m +08.5m  |1.42 |  2.2 | 0.0109 | 38.13 m
 35 |  91 | 171  | (1.05) |508.881 km |308.881  +/-  0.14 km  |86.31 |  2h 28.9m |  212h 12.1m +05.4m  |1.43 |  2.2 | 0.0110 | 38.46 m
 36 |  89 | 167  | (1.08) |517.117 km |317.117  +/-  0.37 km  |86.22 |  2h 32.5m |  212h 13.3m +13.5m  |1.46 |  2.3 | 0.0116 | 40.54 m
 37 |  97 | 182  | (1.18) |517.467 km |317.467  +/-  0.30 km  |86.22 |  2h 32.7m |  231h 32.3m +12.2m  |1.47 |  2.3 | 0.0116 | 40.63 m
 38 |  95 | 178  | (1.21) |525.194 km |325.194  +/-  0.32 km  |86.13 |  2h 36.1m |  231h 32.6m +12.6m  |1.50 |  2.4 | 0.0122 | 42.64 m
 39 |  87 | 163  | (1.11) |525.560 km |325.560  +/-  0.37 km  |86.13 |  2h 36.2m |  212h 14.0m +13.3m  |1.50 |  2.4 | 0.0122 | 42.73 m
 40 |  79 | 148  | (1.01) |525.989 km |325.989  +/-  0.46 km  |86.13 |  2h 36.4m |  192h 54.7m +15.2m  |1.51 |  2.5 | 0.0123 | 42.85 m
 41 |  85 | 159  | (1.14) |534.400 km |334.400  +/-  0.32 km  |86.03 |  2h 40.2m |  212h 17.5m +11.4m  |1.54 |  2.6 | 0.0129 | 45.09 m
 42 |  77 | 144  | (1.04) |535.640 km |335.640  +/-  0.49 km  |86.02 |  2h 40.7m |  192h 52.9m +16.0m  |1.55 |  2.6 | 0.0130 | 45.42 m
 43 |  84 | 157  | (1.16) |538.884 km |338.884  +/-  0.40 km  |85.98 |  2h 42.2m |  212h 14.2m +14.1m  |1.57 |  2.7 | 0.0133 | 46.30 m
 44 |  83 | 155  | (1.17) |543.447 km |343.447  +/-  0.41 km  |85.93 |  2h 44.3m |  212h 12.1m +14.5m  |1.59 |  2.7 | 0.0136 | 47.56 m
 45 |  82 | 153  | (1.19) |548.217 km |348.217  +/-  0.41 km  |85.88 |  2h 46.5m |  212h 13.7m +14.4m  |1.61 |  2.8 | 0.0140 | 48.89 m
 46 |  81 | 151  | (1.21) |553.003 km |353.003  +/-  0.43 km  |85.82 |  2h 48.6m |  212h 11.7m +14.8m  |1.63 |  2.9 | 0.0144 | 50.24 m
 47 |  73 | 136  | (1.11) |556.517 km |356.517  +/-  0.54 km  |85.78 |  2h 50.2m |  192h 55.0m +16.9m  |1.65 |  2.9 | 0.0147 | 51.25 m
 48 |  80 | 149  | (1.22) |557.932 km |357.932  +/-  0.46 km  |85.77 |  2h 50.9m |  212h 10.9m +15.8m  |1.65 |  3.0 | 0.0148 | 51.66 m
 49 |  65 | 121  | (1.01) |560.731 km |360.731  +/-  0.51 km  |85.73 |  2h 52.2m |  173h 36.0m +14.2m  |1.67 |  3.0 | 0.0150 | 52.47 m
 50 |  79 | 147  | (1.24) |563.004 km |363.004  +/-  0.00 km  |85.71 |  2h 53.3m |  212h 19.9m +00.0m  |1.68 |  3.0 | 0.0152 | 53.13 m
 51 |  64 | 119  | (1.03) |567.011 km |367.011  +/-  0.68 km  |85.66 |  2h 55.0m |  173h 33.9m +18.9m  |1.70 |  3.1 | 0.0156 | 54.31 m
 52 |  71 | 132  | (1.14) |567.647 km |367.647  +/-  0.56 km  |85.66 |  2h 55.3m |  192h 52.9m +17.0m  |1.70 |  3.1 | 0.0156 | 54.50 m
 53 |  69 | 128  | (1.18) |579.445 km |379.445  +/-  0.59 km  |85.52 |  3h 00.8m |  192h 53.6m +17.6m  |1.75 |  3.3 | 0.0166 | 58.06 m
 54 |  62 | 115  | (1.06) |580.113 km |380.113  +/-  0.73 km  |85.51 |  3h 01.1m |  173h 34.4m +19.7m  |1.76 |  3.3 | 0.0167 | 58.26 m
 55 |  61 | 113  | (1.08) |586.934 km |386.934  +/-  0.59 km  |85.43 |  3h 04.4m |  173h 36.1m +15.7m  |1.79 |  3.5 | 0.0173 | 60.37 m
 56 |  67 | 124  | (1.22) |591.768 km |391.767  +/-  0.64 km  |85.37 |  3h 06.6m |  192h 51.2m +18.7m  |1.81 |  3.5 | 0.0177 | 61.89 m
 57 |  59 | 109  | (1.12) |601.149 km |401.149  +/-  0.81 km  |85.26 |  3h 11.0m |  173h 31.9m +21.1m  |1.85 |  3.7 | 0.0186 | 64.90 m
 58 |  58 | 107  | (1.14) |608.717 km |408.717  +/-  0.84 km  |85.17 |  3h 14.7m |  173h 34.2m +21.6m  |1.89 |  3.9 | 0.0193 | 67.37 m
 59 |  51 | 94   | (1.03) |613.344 km |413.344  +/-  1.11 km  |85.12 |  3h 16.8m |  154h 10.7m +25.2m  |1.91 |  3.9 | 0.0197 | 68.90 m
 60 |  56 | 103  | (1.19) |624.315 km |424.315  +/-  0.70 km  |84.99 |  3h 22.2m |  173h 35.0m +17.5m  |1.96 |  4.2 | 0.0208 | 72.61 m
 61 |  49 | 90   | (1.07) |631.470 km |431.470  +/-  1.16 km  |84.90 |  3h 25.6m |  154h 12.2m +25.5m  |1.99 |  4.3 | 0.0215 | 75.09 m
 62 |  55 | 101  | (1.21) |632.519 km |432.519  +/-  0.91 km  |84.89 |  3h 26.2m |  173h 32.1m +22.4m  |2.00 |  4.3 | 0.0216 | 75.45 m
 63 |  47 | 86   | (1.12) |650.963 km |450.963  +/-  1.24 km  |84.66 |  3h 35.2m |  154h 13.2m +26.5m  |2.08 |  4.7 | 0.0235 | 82.03 m
 64 |  40 | 73   | (1.01) |664.256 km |464.256  +/-  1.37 km  |84.50 |  3h 41.8m |  134h 55.3m +25.0m  |2.14 |  5.0 | 0.0249 | 86.95 m
 65 |  45 | 82   | (1.17) |672.062 km |472.062  +/-  1.40 km  |84.40 |  3h 45.7m |  154h 14.0m +28.9m  |2.18 |  5.2 | 0.0258 | 89.90 m
 66 |  39 | 71   | (1.03) |676.594 km |476.594  +/-  1.70 km  |84.34 |  3h 47.9m |  134h 51.0m +30.6m  |2.20 |  5.3 | 0.0263 | 91.64 m
 67 |  38 | 69   | (1.06) |689.696 km |489.696  +/-  1.72 km  |84.18 |  3h 54.6m |  134h 52.9m +30.3m  |2.26 |  5.5 | 0.0277 | 96.75 m
 68 |  43 | 78   | (1.22) |694.577 km |494.577  +/-  1.51 km  |84.11 |  3h 57.1m |  154h 07.8m +30.2m  |2.28 |  5.7 | 0.0283 | 98.69 m
 69 |  37 | 67   | (1.09) |703.306 km |503.306  +/-  1.57 km  |84.00 |  4h 01.6m |  134h 53.5m +27.2m  |2.32 |  5.9 | 0.0293 | 0.102 km
 70 |  36 | 65   | (1.11) |717.680 km |517.680  +/-  1.76 km  |83.82 |  4h 09.0m |  134h 52.5m +29.9m  |2.39 |  6.2 | 0.0310 | 0.108 km
 71 |  34 | 61   | (1.18) |748.716 km |548.716  +/-  1.72 km  |83.41 |  4h 25.4m |  134h 53.5m +27.9m  |2.53 |  7.0 | 0.0348 | 0.122 km
 72 |  29 | 52   | (1.01) |751.451 km |551.451  +/-  1.72 km  |83.37 |  4h 26.8m |  115h 37.3m +23.8m  |2.55 |  7.0 | 0.0352 | 0.123 km
 73 |  33 | 59   | (1.21) |765.539 km |565.539  +/-  1.72 km  |83.19 |  4h 34.4m |  134h 53.8m +27.3m  |2.61 |  7.4 | 0.0370 | 0.129 km
 74 |  32 | 57   | (1.24) |783.331 km |583.331  +/-  1.65 km  |82.95 |  4h 44.0m |  134h 54.4m +25.7m  |2.69 |  7.9 | 0.0394 | 0.137 km
 75 |  25 | 44   | (1.16) |839.982 km |639.982  +/-  1.62 km  |82.16 |  5h 15.4m |  115h 39.2m +20.1m  |2.96 |  9.5 | 0.0474 | 0.165 km
 76 |  23 | 40   | (1.24) |895.092 km |695.092  +/-  1.57 km  |81.37 |  5h 47.0m |  115h 40.0m +18.3m  |3.21 | 11.2 | 0.0560 | 0.195 km
 77 |  19 | 33   | (1.04) |901.102 km |701.102  +/-  1.56 km  |81.29 |  5h 50.5m |   96h 23.5m +15.0m  |3.24 | 11.4 | 0.0569 | 0.199 km
 78 |  18 | 31   | (1.09) |939.453 km |739.453  +/-  1.53 km  |80.72 |  6h 13.2m |   96h 24.0m +14.1m  |3.42 | 12.7 | 0.0634 | 0.221 km
 79 |  17 | 29   | (1.10) |982.176 km |782.176  +/-  1.51 km  |80.07 |  6h 38.9m |   96h 24.4m +13.4m  |3.46 | 13.6 | 0.0680 | 0.238 km


Markdown-Formatted Example Output
=================================

Zone | UEC | TEC | Sidelap | SMA | Altitude +/- Range | Inclination | Orbital Period | Time to Scan | Eff. FOV | Swath Width | Resolution (deg) | Resolution (km)
 --- | ----| --- | ------- | --- | ------------------ | ----------- | -------------- | ------------ | -------- | ----------- | ---------------- | ---------------
  1 | 139 | 271  | (1.01) |277.138 km | 77.138  +/-  0.00 km  |88.52 |  0h 59.9m |  135h 11.4m +00.0m  |0.36 |  1.3 | 0.0067 | 23.33 m
  2 | 134 | 261  | (1.06) |284.055 km | 84.055  +/-  0.14 km  |88.46 |  1h 02.1m |  135h 02.9m +06.1m  |0.39 |  1.5 | 0.0073 | 25.42 m
  3 | 132 | 257  | (1.08) |287.044 km | 87.044  +/-  0.17 km  |88.44 |  1h 03.1m |  135h 04.4m +07.4m  |0.40 |  1.5 | 0.0075 | 26.33 m
  4 | 127 | 247  | (1.12) |294.708 km | 94.708  +/-  0.22 km  |88.38 |  1h 05.6m |  135h 02.5m +09.2m  |0.44 |  1.6 | 0.0082 | 28.65 m
  5 | 125 | 243  | (1.14) |297.951 km | 97.951  +/-  0.22 km  |88.35 |  1h 06.7m |  135h 03.3m +09.1m  |0.45 |  1.7 | 0.0085 | 29.63 m
  6 | 103 | 200  | (1.02) |306.108 km |106.108  +/-  0.33 km  |88.28 |  1h 09.4m |  115h 43.0m +11.4m  |0.49 |  1.8 | 0.0092 | 32.10 m
  7 | 120 | 233  | (1.19) |306.410 km |106.410  +/-  0.24 km  |88.28 |  1h 09.5m |  135h 02.5m +09.5m  |0.49 |  1.8 | 0.0092 | 32.19 m
  8 | 118 | 229  | (1.21) |309.972 km |109.972  +/-  0.25 km  |88.25 |  1h 10.8m |  135h 02.7m +10.0m  |0.51 |  1.9 | 0.0095 | 33.26 m
  9 | 101 | 196  | (1.04) |310.290 km |110.290  +/-  0.33 km  |88.25 |  1h 10.9m |  115h 44.2m +11.2m  |0.51 |  1.9 | 0.0096 | 33.36 m
 10 |  97 | 188  | (1.08) |319.003 km |119.003  +/-  0.37 km  |88.17 |  1h 13.9m |  115h 42.9m +11.9m  |0.55 |  2.1 | 0.0103 | 36.00 m
 11 |  95 | 184  | (1.09) |323.630 km |123.630  +/-  0.38 km  |88.13 |  1h 15.5m |  115h 43.6m +12.3m  |0.57 |  2.1 | 0.0107 | 37.40 m
 12 |  91 | 176  | (1.13) |333.329 km |133.329  +/-  0.41 km  |88.05 |  1h 18.9m |  115h 42.2m +12.9m  |0.62 |  2.3 | 0.0116 | 40.33 m
 13 |  89 | 172  | (1.15) |338.512 km |138.512  +/-  0.41 km  |88.00 |  1h 20.7m |  115h 43.4m +12.7m  |0.64 |  2.4 | 0.0120 | 41.90 m
 14 |  85 | 164  | (1.18) |349.404 km |149.404  +/-  0.46 km  |87.90 |  1h 24.7m |  115h 41.8m +13.8m  |0.69 |  2.6 | 0.0129 | 45.20 m
 15 |  83 | 160  | (1.19) |355.239 km |155.239  +/-  0.48 km  |87.85 |  1h 26.8m |  115h 42.9m +14.0m  |0.72 |  2.7 | 0.0135 | 46.96 m
 16 |  69 | 133  | (1.00) |356.177 km |156.177  +/-  0.03 km  |87.84 |  1h 27.2m |   96h 39.7m +00.8m  |0.72 |  2.7 | 0.0135 | 47.25 m
 17 |  68 | 131  | (1.01) |359.580 km |159.580  +/-  0.30 km  |87.81 |  1h 28.4m |   96h 31.0m +07.3m  |0.74 |  2.8 | 0.0138 | 48.28 m
 18 |  67 | 129  | (1.01) |362.982 km |162.982  +/-  0.30 km  |87.78 |  1h 29.7m |   96h 23.8m +07.2m  |0.75 |  2.8 | 0.0141 | 49.31 m
 19 |  66 | 127  | (1.02) |366.894 km |166.894  +/-  0.76 km  |87.74 |  1h 31.0m |   96h 21.2m +18.1m  |0.77 |  2.9 | 0.0145 | 50.49 m
 20 |  79 | 152  | (1.22) |367.562 km |167.562  +/-  0.52 km  |87.74 |  1h 31.3m |  115h 41.3m +14.9m  |0.77 |  2.9 | 0.0145 | 50.69 m
 21 |  77 | 148  | (1.24) |374.192 km |174.192  +/-  0.56 km  |87.68 |  1h 33.8m |  115h 42.0m +15.5m  |0.80 |  3.0 | 0.0151 | 52.70 m
 22 |  64 | 123  | (1.03) |374.892 km |174.892  +/-  0.81 km  |87.67 |  1h 34.0m |   96h 22.6m +18.8m  |0.81 |  3.0 | 0.0152 | 52.91 m
 23 |  63 | 121  | (1.04) |379.057 km |179.057  +/-  0.49 km  |87.63 |  1h 35.7m |   96h 27.4m +11.3m  |0.83 |  3.1 | 0.0155 | 54.17 m
 24 |  62 | 119  | (1.05) |383.128 km |183.128  +/-  0.57 km  |87.59 |  1h 37.2m |   96h 23.0m +13.0m  |0.85 |  3.2 | 0.0159 | 55.41 m
 25 |  61 | 117  | (1.05) |387.516 km |187.516  +/-  0.87 km  |87.55 |  1h 38.8m |   96h 20.3m +19.6m  |0.87 |  3.3 | 0.0163 | 56.74 m
 26 |  59 | 113  | (1.07) |396.690 km |196.690  +/-  0.92 km  |87.46 |  1h 42.3m |   96h 22.0m +20.2m  |0.91 |  3.4 | 0.0170 | 59.51 m
 27 |  58 | 111  | (1.07) |401.413 km |201.413  +/-  0.75 km  |87.42 |  1h 44.2m |   96h 23.2m +16.2m  |0.93 |  3.5 | 0.0175 | 60.94 m
 28 |  57 | 109  | (1.08) |406.278 km |206.278  +/-  0.78 km  |87.37 |  1h 46.1m |   96h 22.3m +16.7m  |0.95 |  3.6 | 0.0179 | 62.42 m
 29 |  56 | 107  | (1.09) |411.287 km |211.287  +/-  1.02 km  |87.32 |  1h 48.0m |   96h 19.3m +21.5m  |0.98 |  3.7 | 0.0183 | 63.93 m
 30 |  54 | 103  | (1.10) |421.971 km |221.971  +/-  1.08 km  |87.22 |  1h 52.3m |   96h 21.0m +22.3m  |1.03 |  3.8 | 0.0192 | 67.17 m
 31 |  53 | 101  | (1.10) |427.489 km |227.489  +/-  0.89 km  |87.16 |  1h 54.5m |   96h 22.4m +18.1m  |1.05 |  3.9 | 0.0197 | 68.84 m
 32 |  52 | 99   | (1.11) |433.181 km |233.181  +/-  0.92 km  |87.11 |  1h 56.8m |   96h 21.3m +18.5m  |1.08 |  4.0 | 0.0202 | 70.56 m
 33 |  51 | 97   | (1.11) |439.080 km |239.080  +/-  1.21 km  |87.05 |  1h 59.1m |   96h 17.9m +23.9m  |1.10 |  4.1 | 0.0207 | 72.35 m
 34 |  49 | 93   | (1.12) |451.720 km |251.720  +/-  1.29 km  |86.92 |  2h 04.3m |   96h 20.0m +24.8m  |1.16 |  4.4 | 0.0218 | 76.18 m
 35 |  48 | 91   | (1.13) |458.271 km |258.271  +/-  1.07 km  |86.85 |  2h 07.1m |   96h 21.4m +20.2m  |1.19 |  4.5 | 0.0224 | 78.17 m
 36 |  47 | 89   | (1.13) |465.060 km |265.060  +/-  1.10 km  |86.78 |  2h 09.9m |   96h 20.4m +20.5m  |1.22 |  4.6 | 0.0230 | 80.22 m
 37 |  46 | 87   | (1.14) |472.104 km |272.104  +/-  1.43 km  |86.71 |  2h 12.8m |   96h 16.5m +26.3m  |1.26 |  4.7 | 0.0236 | 82.36 m
 38 |  44 | 83   | (1.15) |487.305 km |287.305  +/-  1.56 km  |86.55 |  2h 19.2m |   96h 18.5m +27.8m  |1.33 |  5.0 | 0.0249 | 86.96 m
 39 |  43 | 81   | (1.15) |495.255 km |295.255  +/-  1.29 km  |86.46 |  2h 22.7m |   96h 20.3m +22.6m  |1.36 |  5.1 | 0.0256 | 89.37 m
 40 |  42 | 79   | (1.15) |503.522 km |303.522  +/-  1.35 km  |86.37 |  2h 26.3m |   96h 19.0m +23.3m  |1.40 |  5.3 | 0.0263 | 91.88 m
 41 |  41 | 77   | (1.15) |512.140 km |312.140  +/-  1.76 km  |86.28 |  2h 30.0m |   96h 14.6m +29.9m  |1.44 |  5.4 | 0.0271 | 94.49 m
 42 |  39 | 73   | (1.16) |530.839 km |330.839  +/-  1.91 km  |86.07 |  2h 38.3m |   96h 16.6m +31.2m  |1.53 |  5.7 | 0.0287 | 0.100 km
 43 |  38 | 71   | (1.16) |540.729 km |340.728  +/-  1.61 km  |85.96 |  2h 42.8m |   96h 18.7m +25.8m  |1.57 |  5.9 | 0.0296 | 0.103 km
 44 |  37 | 69   | (1.16) |551.048 km |351.048  +/-  1.69 km  |85.84 |  2h 47.5m |   96h 17.2m +26.6m  |1.62 |  6.1 | 0.0304 | 0.106 km
 45 |  36 | 67   | (1.17) |562.003 km |362.003  +/-  1.99 km  |85.72 |  2h 52.4m |   96h 15.6m +30.7m  |1.67 |  6.3 | 0.0314 | 0.110 km
 46 |  34 | 63   | (1.17) |585.551 km |385.551  +/-  1.96 km  |85.45 |  3h 03.4m |   96h 16.6m +29.0m  |1.78 |  6.7 | 0.0334 | 0.117 km
 47 |  33 | 61   | (1.17) |598.271 km |398.271  +/-  1.94 km  |85.30 |  3h 09.4m |   96h 17.0m +28.2m  |1.84 |  6.9 | 0.0346 | 0.121 km
 48 |  32 | 59   | (1.17) |611.722 km |411.722  +/-  1.92 km  |85.14 |  3h 15.8m |   96h 17.4m +27.3m  |1.90 |  7.1 | 0.0357 | 0.125 km
 49 |  31 | 57   | (1.17) |625.952 km |425.952  +/-  1.89 km  |84.97 |  3h 22.7m |   96h 17.9m +26.3m  |1.97 |  7.4 | 0.0370 | 0.129 km
 50 |  29 | 53   | (1.17) |657.053 km |457.053  +/-  1.84 km  |84.59 |  3h 38.1m |   96h 18.9m +24.4m  |2.11 |  7.9 | 0.0397 | 0.138 km
 51 |  28 | 51   | (1.16) |674.114 km |474.114  +/-  1.81 km  |84.37 |  3h 46.6m |   96h 19.3m +23.4m  |2.19 |  8.2 | 0.0412 | 0.144 km
 52 |  27 | 49   | (1.16) |692.351 km |492.351  +/-  1.80 km  |84.14 |  3h 55.9m |   96h 19.8m +22.5m  |2.27 |  8.5 | 0.0427 | 0.149 km
 53 |  26 | 47   | (1.16) |711.844 km |511.844  +/-  1.78 km  |83.89 |  4h 06.0m |   96h 20.2m +21.7m  |2.36 |  8.9 | 0.0444 | 0.155 km
 54 |  24 | 43   | (1.15) |755.331 km |555.331  +/-  1.72 km  |83.32 |  4h 28.9m |   96h 21.1m +19.7m  |2.56 |  9.6 | 0.0482 | 0.168 km
 55 |  23 | 41   | (1.15) |779.706 km |579.706  +/-  1.70 km  |83.00 |  4h 42.0m |   96h 21.5m +19.0m  |2.68 | 10.1 | 0.0504 | 0.176 km
 56 |  22 | 39   | (1.14) |806.131 km |606.131  +/-  1.65 km  |82.63 |  4h 56.5m |   96h 22.1m +17.8m  |2.80 | 10.5 | 0.0527 | 0.184 km
 57 |  21 | 37   | (1.13) |834.926 km |634.926  +/-  1.62 km  |82.23 |  5h 12.6m |   96h 22.6m +16.9m  |2.93 | 11.0 | 0.0552 | 0.193 km
 58 |  19 | 33   | (1.12) |901.102 km |701.102  +/-  1.56 km  |81.29 |  5h 50.5m |   96h 23.5m +15.0m  |3.24 | 12.2 | 0.0609 | 0.213 km
 59 |  18 | 31   | (1.11) |939.453 km |739.453  +/-  1.53 km  |80.72 |  6h 13.2m |   96h 24.0m +14.1m  |3.42 | 12.9 | 0.0643 | 0.224 km
 60 |  17 | 29   | (1.10) |982.176 km |782.176  +/-  1.51 km  |80.07 |  6h 38.9m |   96h 24.4m +13.4m  |3.46 | 13.6 | 0.0680 | 0.238 km



