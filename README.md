# NYC Taxi Zone CSV to Parquet (PySpark)

This project is a small local PySpark workflow that converts the NYC taxi zone lookup dataset from CSV format into Parquet format.

## What Is Happening in This Project

The notebook (`conversion.ipynb`, same content as `Untitled.ipynb`) does the following:

1. Imports `pyspark`, `os`, and `sys`.
2. Sets Windows Hadoop-related paths:
   - `HADOOP_HOME = C:/hadoop`
   - Adds `C:/hadoop/bin` to `sys.path`
3. Creates a local Spark session:
   - `master("local[*]")`
   - App name: `test`
4. Downloads `taxi_zone_lookup.csv` (the notebook first tries one URL, then uses a working fallback URL).
5. Reads the CSV with header enabled into a Spark DataFrame.
6. Displays sample rows with `df.show()`.
7. Writes the DataFrame to Parquet in `zones/` using overwrite mode:
   - `df.write.mode("overwrite").parquet("zones")`

## Project Files

- `conversion.ipynb`: Main notebook with the CSV-to-Parquet process.
- `Untitled.ipynb`: Duplicate of `conversion.ipynb`.
- `taxi_zone_lookup.csv`: Input dataset (266 lines including header).
- `zones/`: Spark Parquet output directory (`part-*.parquet`, `_SUCCESS`, and CRC files).

## Prerequisites

- Python 3.x
- Java (required by Spark)
- `pyspark`
- Jupyter Notebook
- Windows Hadoop/winutils setup if running exactly as written (`C:/hadoop`)

Install core Python packages:

```bash
pip install pyspark jupyter
```

## How to Run

1. Open the project folder.
2. Start Jupyter:

```bash
jupyter notebook
```

3. Open `conversion.ipynb`.
4. Run all cells in order.
5. Confirm `zones/` is created/updated with Parquet output.

## Notes

- `conversion.ipynb` and `Untitled.ipynb` are currently identical.
- Output is written with overwrite mode, so reruns replace existing Parquet files in `zones/`.
