# LIMPIEZA DE LOS DATOS DE INDICE DE PRECIOS POR TRIMESTRE


```python
import pandas as pd
```


```python
ruta_archivo = "Indice SHF datos abiertos 3_trim_2025.xlsx"

df = pd.read_excel(ruta_archivo)
```


```python
df = df.iloc[:, 2:]
```


```python
df_cdmx = df[df["Estado"] == "Ciudad de México"].copy()
```


```python
df_cdmx.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Estado</th>
      <th>Municipio</th>
      <th>Trimestre</th>
      <th>Año</th>
      <th>Indice</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>23</th>
      <td>Ciudad de México</td>
      <td>NaN</td>
      <td>1</td>
      <td>2005</td>
      <td>33.81</td>
    </tr>
    <tr>
      <th>63</th>
      <td>Ciudad de México</td>
      <td>Gustavo A. Madero</td>
      <td>1</td>
      <td>2005</td>
      <td>34.33</td>
    </tr>
    <tr>
      <th>64</th>
      <td>Ciudad de México</td>
      <td>Iztapalapa</td>
      <td>1</td>
      <td>2005</td>
      <td>35.49</td>
    </tr>
    <tr>
      <th>65</th>
      <td>Ciudad de México</td>
      <td>Benito Juárez</td>
      <td>1</td>
      <td>2005</td>
      <td>33.14</td>
    </tr>
    <tr>
      <th>66</th>
      <td>Ciudad de México</td>
      <td>Cuauhtémoc</td>
      <td>1</td>
      <td>2005</td>
      <td>32.77</td>
    </tr>
  </tbody>
</table>
</div>




```python
ruta_salida = "Indice_SHF_CDMX.xlsx"
df_cdmx.to_excel(ruta_salida, index=False)
```

# LIMPIEZA DE CODIGOS POSTALES


```python
ruta_cp = "CodigosPostales.xlsx"

cp = pd.read_excel(
    ruta_cp,
    header=1,
    dtype={"Código Postal": str}
)
```


```python
cp.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Código Postal</th>
      <th>Estado</th>
      <th>Municipio</th>
      <th>Ciudad</th>
      <th>Tipo de Asentamiento</th>
      <th>Asentamiento</th>
      <th>Clave de Oficina</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3103</td>
      <td>Ciudad de México</td>
      <td>Benito Juárez</td>
      <td>Ciudad de México</td>
      <td>Colonia</td>
      <td>Del Valle Norte</td>
      <td>3001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3104</td>
      <td>Ciudad de México</td>
      <td>Benito Juárez</td>
      <td>Ciudad de México</td>
      <td>Colonia</td>
      <td>Del Valle Sur</td>
      <td>3001</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3200</td>
      <td>Ciudad de México</td>
      <td>Benito Juárez</td>
      <td>Ciudad de México</td>
      <td>Colonia</td>
      <td>Tlacoquemécatl</td>
      <td>3001</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3230</td>
      <td>Ciudad de México</td>
      <td>Benito Juárez</td>
      <td>Ciudad de México</td>
      <td>Colonia</td>
      <td>Actipan</td>
      <td>3001</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3240</td>
      <td>Ciudad de México</td>
      <td>Benito Juárez</td>
      <td>Ciudad de México</td>
      <td>Colonia</td>
      <td>Acacias</td>
      <td>3001</td>
    </tr>
  </tbody>
</table>
</div>




```python
cp_cdmx = cp[["Código Postal", "Municipio"]].copy()

cp_cdmx = cp_cdmx.rename(columns={
    "Código Postal": "codigo_postal",
    "Municipio": "alcaldia"
})
```


```python
cp["Código Postal"] = cp["Código Postal"].astype(str).str.strip()
cp["Municipio"] = cp["Municipio"].astype(str).str.strip()

```


```python
cp_sin_duplicados = cp.drop_duplicates(
    subset=["Código Postal", "Municipio"]
).copy()

```


```python
cp_sin_duplicados.to_excel(
    "CodigosPostales_CDMX_sin_duplicados.xlsx",
    index=False
)
```


```python
print("Filas originales:", len(cp))
print("Filas sin duplicados:", len(cp_sin_duplicados))
print("CP únicos:", cp_sin_duplicados["Código Postal"].nunique())
print("Alcaldías únicas:", cp_sin_duplicados["Municipio"].nunique())

cp_sin_duplicados.head()

```

    Filas originales: 1529
    Filas sin duplicados: 1110
    CP únicos: 1110
    Alcaldías únicas: 16
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Código Postal</th>
      <th>Estado</th>
      <th>Municipio</th>
      <th>Ciudad</th>
      <th>Tipo de Asentamiento</th>
      <th>Asentamiento</th>
      <th>Clave de Oficina</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3103</td>
      <td>Ciudad de México</td>
      <td>Benito Juárez</td>
      <td>Ciudad de México</td>
      <td>Colonia</td>
      <td>Del Valle Norte</td>
      <td>3001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3104</td>
      <td>Ciudad de México</td>
      <td>Benito Juárez</td>
      <td>Ciudad de México</td>
      <td>Colonia</td>
      <td>Del Valle Sur</td>
      <td>3001</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3200</td>
      <td>Ciudad de México</td>
      <td>Benito Juárez</td>
      <td>Ciudad de México</td>
      <td>Colonia</td>
      <td>Tlacoquemécatl</td>
      <td>3001</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3230</td>
      <td>Ciudad de México</td>
      <td>Benito Juárez</td>
      <td>Ciudad de México</td>
      <td>Colonia</td>
      <td>Actipan</td>
      <td>3001</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3240</td>
      <td>Ciudad de México</td>
      <td>Benito Juárez</td>
      <td>Ciudad de México</td>
      <td>Colonia</td>
      <td>Acacias</td>
      <td>3001</td>
    </tr>
  </tbody>
</table>
</div>


