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


Example Markdown Output
=======================

  UEQx | EQx|Sidelap| Altitude |    Error  | Inc.    | O. Period| Scan Time |    Error| FOV  |Swath|Res (°)|Res (m)
-------|----|-------|----------|-----------|---------|----------|-----------|---------|------|-----|-------|--------
   17|   29|(1.10)| 782.176 km|+/- 1.51 km|(80.07°)|  6h 38.9m|   96h 24.4m|+/- 13.4m|(3.5°)| 14 m|(0.07°)|0.238 km
   18|   31|(1.09)| 739.453 km|+/- 1.53 km|(80.72°)|  6h 13.2m|   96h 24.0m|+/- 14.1m|(3.4°)| 13 m|(0.06°)|0.221 km
   19|   33|(1.04)| 701.102 km|+/- 1.56 km|(81.29°)|  5h 50.5m|   96h 23.5m|+/- 15.0m|(3.2°)| 11 m|(0.06°)|0.199 km
   23|   40|(1.24)| 695.092 km|+/- 1.57 km|(81.37°)|  5h 47.0m|  115h 40.0m|+/- 18.3m|(3.2°)| 11 m|(0.06°)|0.195 km
   25|   44|(1.16)| 639.982 km|+/- 1.62 km|(82.16°)|  5h 15.4m|  115h 39.2m|+/- 20.1m|(3.0°)|  9 m|(0.05°)|0.165 km
   32|   57|(1.24)| 583.331 km|+/- 1.65 km|(82.95°)|  4h 44.0m|  134h 54.4m|+/- 25.7m|(2.7°)|  8 m|(0.04°)|0.137 km
   33|   59|(1.21)| 565.539 km|+/- 1.72 km|(83.19°)|  4h 34.4m|  134h 53.8m|+/- 27.3m|(2.6°)|  7 m|(0.04°)|0.129 km
   29|   52|(1.01)| 551.451 km|+/- 1.72 km|(83.37°)|  4h 26.8m|  115h 37.3m|+/- 23.8m|(2.5°)|  7 m|(0.04°)|0.123 km
   34|   61|(1.18)| 548.716 km|+/- 1.72 km|(83.41°)|  4h 25.4m|  134h 53.5m|+/- 27.9m|(2.5°)|  7 m|(0.03°)|0.122 km
   36|   65|(1.11)| 517.680 km|+/- 1.76 km|(83.82°)|  4h 09.0m|  134h 52.5m|+/- 29.9m|(2.4°)|  6 m|(0.03°)|0.108 km
   37|   67|(1.09)| 503.306 km|+/- 1.57 km|(84.00°)|  4h 01.6m|  134h 53.5m|+/- 27.2m|(2.3°)|  6 m|(0.03°)|0.102 km
   43|   78|(1.22)| 494.577 km|+/- 1.51 km|(84.11°)|  3h 57.1m|  154h 07.8m|+/- 30.2m|(2.3°)|  6 m|(0.03°)|98.69 m
   38|   69|(1.06)| 489.696 km|+/- 1.72 km|(84.18°)|  3h 54.6m|  134h 52.9m|+/- 30.3m|(2.3°)|  6 m|(0.03°)|96.75 m
   39|   71|(1.03)| 476.594 km|+/- 1.70 km|(84.34°)|  3h 47.9m|  134h 51.0m|+/- 30.6m|(2.2°)|  5 m|(0.03°)|91.64 m
   45|   82|(1.17)| 472.062 km|+/- 1.40 km|(84.40°)|  3h 45.7m|  154h 14.0m|+/- 28.9m|(2.2°)|  5 m|(0.03°)|89.90 m
   40|   73|(1.01)| 464.256 km|+/- 1.37 km|(84.50°)|  3h 41.8m|  134h 55.3m|+/- 25.0m|(2.1°)|  5 m|(0.02°)|86.95 m
   47|   86|(1.12)| 450.963 km|+/- 1.24 km|(84.66°)|  3h 35.2m|  154h 13.2m|+/- 26.5m|(2.1°)|  5 m|(0.02°)|82.03 m
   55|  101|(1.21)| 432.519 km|+/- 0.91 km|(84.89°)|  3h 26.2m|  173h 32.1m|+/- 22.4m|(2.0°)|  4 m|(0.02°)|75.45 m
   49|   90|(1.07)| 431.470 km|+/- 1.16 km|(84.90°)|  3h 25.6m|  154h 12.2m|+/- 25.5m|(2.0°)|  4 m|(0.02°)|75.09 m
   56|  103|(1.19)| 424.315 km|+/- 0.70 km|(84.99°)|  3h 22.2m|  173h 35.0m|+/- 17.5m|(2.0°)|  4 m|(0.02°)|72.61 m
   51|   94|(1.03)| 413.344 km|+/- 1.11 km|(85.12°)|  3h 16.8m|  154h 10.7m|+/- 25.2m|(1.9°)|  4 m|(0.02°)|68.90 m
   58|  107|(1.14)| 408.717 km|+/- 0.84 km|(85.17°)|  3h 14.7m|  173h 34.2m|+/- 21.6m|(1.9°)|  4 m|(0.02°)|67.37 m
   59|  109|(1.12)| 401.149 km|+/- 0.81 km|(85.26°)|  3h 11.0m|  173h 31.9m|+/- 21.1m|(1.9°)|  4 m|(0.02°)|64.90 m
   67|  124|(1.22)| 391.767 km|+/- 0.64 km|(85.37°)|  3h 06.6m|  192h 51.2m|+/- 18.7m|(1.8°)|  4 m|(0.02°)|61.89 m
   61|  113|(1.08)| 386.934 km|+/- 0.59 km|(85.43°)|  3h 04.4m|  173h 36.1m|+/- 15.7m|(1.8°)|  3 m|(0.02°)|60.37 m
   62|  115|(1.06)| 380.113 km|+/- 0.73 km|(85.51°)|  3h 01.1m|  173h 34.4m|+/- 19.7m|(1.8°)|  3 m|(0.02°)|58.26 m
   69|  128|(1.18)| 379.445 km|+/- 0.59 km|(85.52°)|  3h 00.8m|  192h 53.6m|+/- 17.6m|(1.8°)|  3 m|(0.02°)|58.06 m
   71|  132|(1.14)| 367.647 km|+/- 0.56 km|(85.66°)|  2h 55.3m|  192h 52.9m|+/- 17.0m|(1.7°)|  3 m|(0.02°)|54.50 m
   64|  119|(1.03)| 367.011 km|+/- 0.68 km|(85.66°)|  2h 55.0m|  173h 33.9m|+/- 18.9m|(1.7°)|  3 m|(0.02°)|54.31 m
   79|  147|(1.24)| 363.004 km|+/- 0.00 km|(85.71°)|  2h 53.3m|  212h 19.9m|+/- 00.0m|(1.7°)|  3 m|(0.02°)|53.13 m
   65|  121|(1.01)| 360.731 km|+/- 0.51 km|(85.73°)|  2h 52.2m|  173h 36.0m|+/- 14.2m|(1.7°)|  3 m|(0.02°)|52.47 m
   80|  149|(1.22)| 357.932 km|+/- 0.46 km|(85.77°)|  2h 50.9m|  212h 10.9m|+/- 15.8m|(1.7°)|  3 m|(0.01°)|51.66 m
   73|  136|(1.11)| 356.517 km|+/- 0.54 km|(85.78°)|  2h 50.2m|  192h 55.0m|+/- 16.9m|(1.6°)|  3 m|(0.01°)|51.25 m
   81|  151|(1.21)| 353.003 km|+/- 0.43 km|(85.82°)|  2h 48.6m|  212h 11.7m|+/- 14.8m|(1.6°)|  3 m|(0.01°)|50.24 m
   82|  153|(1.19)| 348.217 km|+/- 0.41 km|(85.88°)|  2h 46.5m|  212h 13.7m|+/- 14.4m|(1.6°)|  3 m|(0.01°)|48.89 m
   83|  155|(1.17)| 343.447 km|+/- 0.41 km|(85.93°)|  2h 44.3m|  212h 12.1m|+/- 14.5m|(1.6°)|  3 m|(0.01°)|47.56 m
   84|  157|(1.16)| 338.884 km|+/- 0.40 km|(85.98°)|  2h 42.2m|  212h 14.2m|+/- 14.1m|(1.6°)|  3 m|(0.01°)|46.30 m
   77|  144|(1.04)| 335.640 km|+/- 0.49 km|(86.02°)|  2h 40.7m|  192h 52.9m|+/- 16.0m|(1.6°)|  3 m|(0.01°)|45.42 m
   85|  159|(1.14)| 334.400 km|+/- 0.32 km|(86.03°)|  2h 40.2m|  212h 17.5m|+/- 11.4m|(1.5°)|  3 m|(0.01°)|45.09 m
   79|  148|(1.01)| 325.989 km|+/- 0.46 km|(86.13°)|  2h 36.4m|  192h 54.7m|+/- 15.2m|(1.5°)|  2 m|(0.01°)|42.85 m
   87|  163|(1.11)| 325.560 km|+/- 0.37 km|(86.13°)|  2h 36.2m|  212h 14.0m|+/- 13.3m|(1.5°)|  2 m|(0.01°)|42.73 m
   95|  178|(1.21)| 325.194 km|+/- 0.32 km|(86.13°)|  2h 36.1m|  231h 32.6m|+/- 12.6m|(1.5°)|  2 m|(0.01°)|42.64 m
   97|  182|(1.18)| 317.467 km|+/- 0.30 km|(86.22°)|  2h 32.7m|  231h 32.3m|+/- 12.2m|(1.5°)|  2 m|(0.01°)|40.63 m
   89|  167|(1.08)| 317.117 km|+/- 0.37 km|(86.22°)|  2h 32.5m|  212h 13.3m|+/- 13.5m|(1.5°)|  2 m|(0.01°)|40.54 m
   91|  171|(1.05)| 308.881 km|+/- 0.14 km|(86.31°)|  2h 28.9m|  212h 12.1m|+/- 05.4m|(1.4°)|  2 m|(0.01°)|38.46 m
  108|  203|(1.23)| 307.545 km|+/- 0.19 km|(86.33°)|  2h 28.3m|  250h 54.5m|+/- 08.5m|(1.4°)|  2 m|(0.01°)|38.13 m
   92|  173|(1.03)| 305.065 km|+/- 0.35 km|(86.35°)|  2h 27.2m|  212h 12.7m|+/- 13.2m|(1.4°)|  2 m|(0.01°)|37.52 m
   93|  175|(1.02)| 301.249 km|+/- 0.35 km|(86.40°)|  2h 25.5m|  212h 14.2m|+/- 13.3m|(1.4°)|  2 m|(0.01°)|36.59 m
  110|  207|(1.20)| 300.947 km|+/- 0.22 km|(86.40°)|  2h 25.4m|  250h 52.0m|+/- 10.0m|(1.4°)|  2 m|(0.01°)|36.51 m
  111|  209|(1.19)| 297.735 km|+/- 0.24 km|(86.43°)|  2h 24.0m|  250h 50.7m|+/- 10.8m|(1.4°)|  2 m|(0.01°)|35.74 m
   94|  177|(1.00)| 297.433 km|+/- 0.32 km|(86.44°)|  2h 23.9m|  212h 13.5m|+/- 12.2m|(1.4°)|  2 m|(0.01°)|35.67 m
  113|  213|(1.16)| 291.407 km|+/- 0.08 km|(86.50°)|  2h 21.3m|  250h 50.7m|+/- 03.7m|(1.3°)|  2 m|(0.01°)|34.23 m
  107|  202|(1.04)| 282.725 km|+/- 0.24 km|(86.59°)|  2h 17.6m|  231h 33.4m|+/- 10.3m|(1.3°)|  2 m|(0.01°)|32.22 m
  116|  219|(1.12)| 282.487 km|+/- 0.21 km|(86.60°)|  2h 17.5m|  250h 52.3m|+/- 09.7m|(1.3°)|  2 m|(0.01°)|32.17 m
  125|  236|(1.21)| 282.264 km|+/- 0.19 km|(86.60°)|  2h 17.4m|  270h 10.3m|+/- 09.6m|(1.3°)|  2 m|(0.01°)|32.12 m
  127|  240|(1.18)| 276.890 km|+/- 0.17 km|(86.66°)|  2h 15.1m|  270h 10.2m|+/- 08.9m|(1.3°)|  2 m|(0.01°)|30.91 m
  118|  223|(1.09)| 276.683 km|+/- 0.21 km|(86.66°)|  2h 15.0m|  250h 51.4m|+/- 09.8m|(1.3°)|  2 m|(0.01°)|30.86 m
  109|  206|(1.01)| 276.445 km|+/- 0.24 km|(86.66°)|  2h 14.9m|  231h 32.9m|+/- 10.4m|(1.3°)|  2 m|(0.01°)|30.81 m
  123|  233|(1.03)| 262.946 km|+/- 0.19 km|(86.80°)|  2h 09.2m|  250h 52.1m|+/- 09.3m|(1.2°)|  2 m|(0.01°)|27.87 m
  142|  269|(1.19)| 262.787 km|+/- 0.10 km|(86.80°)|  2h 09.2m|  289h 31.5m|+/- 05.4m|(1.2°)|  2 m|(0.01°)|27.84 m
  143|  271|(1.18)| 260.465 km|+/- 0.10 km|(86.83°)|  2h 08.2m|  289h 29.1m|+/- 05.4m|(1.2°)|  2 m|(0.01°)|27.35 m
  124|  235|(1.02)| 260.306 km|+/- 0.19 km|(86.83°)|  2h 08.1m|  250h 51.6m|+/- 09.4m|(1.2°)|  2 m|(0.01°)|27.32 m
  139|  264|(1.04)| 247.539 km|+/- 0.14 km|(86.96°)|  2h 02.8m|  270h 11.2m|+/- 07.8m|(1.1°)|  1 m|(0.01°)|24.70 m
  149|  283|(1.11)| 247.380 km|+/- 0.13 km|(86.96°)|  2h 02.8m|  289h 29.5m|+/- 07.4m|(1.1°)|  1 m|(0.01°)|24.67 m
  159|  302|(1.18)| 247.252 km|+/- 0.11 km|(86.96°)|  2h 02.7m|  308h 47.8m|+/- 06.9m|(1.1°)|  1 m|(0.01°)|24.64 m
  171|  325|(1.24)| 243.452 km|+/- 0.10 km|(87.00°)|  2h 01.1m|  328h 06.3m|+/- 06.4m|(1.1°)|  1 m|(0.01°)|23.89 m
  161|  306|(1.16)| 243.341 km|+/- 0.11 km|(87.00°)|  2h 01.1m|  308h 47.4m|+/- 07.0m|(1.1°)|  1 m|(0.01°)|23.87 m
  151|  287|(1.09)| 243.214 km|+/- 0.11 km|(87.00°)|  2h 01.0m|  289h 29.5m|+/- 06.5m|(1.1°)|  1 m|(0.01°)|23.85 m
  141|  268|(1.02)| 243.071 km|+/- 0.14 km|(87.01°)|  2h 01.0m|  270h 10.9m|+/- 07.9m|(1.1°)|  1 m|(0.01°)|23.82 m
  175|  334|(1.02)| 218.203 km|+/- 0.10 km|(87.25°)|  1h 50.9m|  308h 48.2m|+/- 06.3m|(1.0°)|  1 m|(0.01°)|19.19 m
  186|  355|(1.08)| 218.108 km|+/- 0.08 km|(87.26°)|  1h 50.9m|  328h 06.4m|+/- 05.6m|(1.0°)|  1 m|(0.01°)|19.18 m
  197|  376|(1.15)| 218.012 km|+/- 0.06 km|(87.26°)|  1h 50.9m|  347h 25.0m|+/- 04.8m|(1.0°)|  1 m|(0.01°)|19.16 m
  208|  397|(1.21)| 217.949 km|+/- 0.05 km|(87.26°)|  1h 50.9m|  366h 44.2m|+/- 03.8m|(1.0°)|  1 m|(0.01°)|19.15 m
  210|  401|(1.19)| 215.150 km|+/- 0.06 km|(87.28°)|  1h 49.7m|  366h 43.0m|+/- 05.1m|(1.0°)|  1 m|(0.01°)|18.66 m
  199|  380|(1.13)| 215.071 km|+/- 0.06 km|(87.29°)|  1h 49.7m|  347h 24.8m|+/- 04.8m|(1.0°)|  1 m|(0.01°)|18.65 m
  188|  359|(1.06)| 214.991 km|+/- 0.06 km|(87.29°)|  1h 49.7m|  328h 07.2m|+/- 04.5m|(1.0°)|  1 m|(0.01°)|18.63 m
  177|  338|(1.00)| 214.896 km|+/- 0.10 km|(87.29°)|  1h 49.6m|  308h 48.1m|+/- 06.4m|(1.0°)|  1 m|(0.01°)|18.62 m
  227|  435|(1.04)| 193.256 km|+/- 0.02 km|(87.50°)|  1h 41.2m|  366h 46.8m|+/- 01.3m|(0.9°)|  1 m|(0.00°)|15.05 m
  229|  439|(1.03)| 190.807 km|+/- 0.02 km|(87.52°)|  1h 40.2m|  366h 43.3m|+/- 01.3m|(0.9°)|  1 m|(0.00°)|14.68 m

