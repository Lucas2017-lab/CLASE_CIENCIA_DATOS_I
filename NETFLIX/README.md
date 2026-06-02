# INTELIGENCIA DE DATOS DE NETFLIX
INTRODUCCIÓN Y PROPÓSITO DEL ANÁLISIS
El propósito de este proyecto es mitigar el riesgo de inversión en un mercado de streaming saturado mediante la transformación de los hábitos de consumo en indicadores de inteligencia de negocios . El estudio se centra en el mercado de Norteamérica (Estados Unidos y Canadá), identificando nichos de alta eficiencia y anclas de retención para optimizar la toma de decisiones financieras con proyecciones al cierre de 2026

from google.colab import files
upload  = files.upload()

import pandas as pd
df = pd.read_csv("netflix_cleaned_20251011_141144.csv")

### EVALUCIÓN DE VISTAS POR GÉNERO ###

df["genre_primary"].value_counts()

### EVALUCIÓN DE VISTAS POR PAÍS ###
df["country"].value_counts()

### EVALUCIÓN DE VISTAS POR CIUDAD DE CANADÁ ###
df["city"].value_counts()

### EVALUCIÓN DE VISTAS POR ESTADO DE EEUU ###
df["state_province"].value_counts()

### ANÁLISIS DE GENERO VE CADA MÁS CADA PAÍS ###
generos_paises = df.groupby("country")["genre_primary"].describe()
preferencias_paises = generos_paises[["top"]].reset_index()
preferencias_paises.columns = ["País", "Genero Favorito"]
preferencias_paises

### SEGMENTACIÓN DEL NUESTRO ANALISIS ENTRE LAS CIUDADES Y ESTADOS DEL OESTE Y EL ESTE ###
### SEGMENTACIÓN DEL ESTE ###
eastern_provinces_states = [
    'North Carolina', 'Tennessee', 'Indiana', 'Michigan', 'Florida', 'Illinois', 'Georgia',
    'Massachusetts', 'Maryland', 'New York', 'New Jersey', 'Ohio', 'Virginia', 'Pennsylvania',
    'Nova Scotia', 'Quebec', 'Prince Edward Island', 'Newfoundland and Labrador', 'New Brunswick',
    'Wisconsin', 'Ontario'
]
### SEGMENTACIÓN DEL OESTE ###
western_provinces_states = [
    'Texas', 'California', 'Missouri', 'Washington', 'Arizona',
    'Manitoba', 'Alberta', 'British Columbia', 'Saskatchewan'
]

# Creamos DataFrame para estados del Este
df_eastern = df[df['state_province'].isin(eastern_provinces_states)]

# 2. El cambio está aquí: usamos df_eastern en lugar de df_western
resumen_generos = df_eastern.groupby('state_province')['genre_primary'].describe()

# 3. Extraemos el valor más frecuente ('top') o el genero mas visto
preferencias_este = resumen_generos[['top']].reset_index()

# 4. Renombramos para que sea auto-explicativo
preferencias_este.columns = ['Estado / Provincia', 'Género Favorito']

preferencias_este

# Creamos DataFrame para estados del Oeste
# Filtramos primero (ojo con no cruzar las variables aquí)
df_western = df[df['state_province'].isin(western_provinces_states)]

# Sacamos el conteo del oeste
top3_oeste = df_western['genre_primary'].value_counts().head(3).reset_index()

# Renombramos columnas
top3_oeste.columns = ['Género (Oeste)', 'Cantidad de Visualizaciones']

print("\n--- TOP 3 GÉNEROS EN EL OESTE ---")
display(top3_oeste)








### SEGMENTACIÓN GEOGRÁFICA DEL ANALISIS ###
