# PRISM datasets

Processed urban sensing datasets used in the paper "PRISM: Multi-Scale Spatial Reasoning via Hop-Decomposed Attention for Lightweight Forecasting in Urban IoT Sensing" by Shiyu Yang, Haojie Chen, Chuxi Fan, Ming Xue, Yumo Chen, and Qunyong Wu.

| Folder | Variable | Nodes | Interval | Steps | Period | Time of the series |
|---|---|---|---|---|---|---|
| `Traffic` | Vehicle counts from automatic vehicle identification cameras in Wuhan, China [1] | 67 | 5 min | 8064 | 2021-03-01 to 2021-03-28 | Local time (UTC+8) |
| `PM2.5` | Hourly PM2.5 concentration (µg/m³) at air-quality monitoring stations in Beijing, China, and its surrounding districts [2] | 36 | 60 min | 2952 | 2014-05-01 to 2014-08-31 | Local time (UTC+8) |
| `Temperature` | 2-m air temperature (°C) from the ERA5 reanalysis [3] on grid cells covering Wuhan and its surrounding region | 64 | 60 min | 2208 | 2018-06-01 to 2018-08-31 | UTC |

## Files

Each folder contains two comma-separated files without a header.

- `series.csv`: one row per node and one column per time step (nodes × steps). The columns are consecutive time steps covering the full days of the period.
- `adjacency.csv`: a binary nodes × nodes matrix whose rows and columns follow the node order of `series.csv`. Entry (i, j) is 1 when node j is node i itself or one of the ten nodes most similar to node i, and 0 otherwise, so every row contains eleven ones. The matrix is not symmetric.

## Missing values

The missing entries of the raw Traffic and PM2.5 records (8.94% and 10.35% of the raw records) were filled with the Bayesian temporal tensor factorization model [4] when the datasets were assembled; the Temperature data have no missing entries. In the series, zero values are treated as missing: in the paper they are excluded from the training loss and from all evaluation metrics.

## Protocol used in the paper

Each series is split chronologically into training, validation, and test sets with a 60%/20%/20% ratio. Models take six input steps and forecast the next six steps; inputs are normalized with a z-score scaler fitted on the training set.

## Sources

1. P. Wang, T. Zhang, H. Zhang, S. Cheng, and W. Wang, "Adding attention to the neural ordinary differential equation for spatio-temporal prediction," *International Journal of Geographical Information Science*, vol. 38, no. 1, pp. 156–181, 2024. https://doi.org/10.1080/13658816.2023.2275160
2. Y. Zheng, X. Yi, M. Li, R. Li, Z. Shan, E. Chang, and T. Li, "Forecasting fine-grained air quality based on big data," in *Proceedings of the 21th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining*, 2015, pp. 2267–2276. https://doi.org/10.1145/2783258.2788573
3. H. Hersbach et al., "The ERA5 global reanalysis," *Quarterly Journal of the Royal Meteorological Society*, vol. 146, no. 730, pp. 1999–2049, 2020. https://doi.org/10.1002/qj.3803
4. X. Chen and L. Sun, "Bayesian temporal factorization for multidimensional time series prediction," *IEEE Transactions on Pattern Analysis and Machine Intelligence*, vol. 44, no. 9, pp. 4659–4673, 2022. https://doi.org/10.1109/TPAMI.2021.3066551
