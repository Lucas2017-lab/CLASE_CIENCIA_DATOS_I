
INTELIGENCIA DE DATOS DE NETFLIX
INTRODUCCIÓN Y PROPÓSITO DEL ANÁLISIS El propósito de este proyecto es mitigar el riesgo de inversión en un mercado de streaming saturado mediante la transformación de los hábitos de consumo en indicadores de inteligencia de negocios. El estudio se centra en el mercado de Norteamérica (Estados Unidos y Canadá), identificando nichos de alta eficiencia y anclas de retención para optimizar la toma de decisiones financieras con proyecciones al cierre de 2026.

from google.colab import files upload = files.upload()

import pandas as pd df = pd.read_csv("netflix_cleaned_20251011_141144.csv")

EVALUCIÓN DE VISTAS POR GÉNERO
df["genre_primary"].value_counts()

EVALUCIÓN DE VISTAS POR PAÍS
df["country"].value_counts()

EVALUCIÓN DE VISTAS POR CIUDAD DE CANADÁ
df["ciudad"].value_counts()

EVALUCIÓN DE VISTAS POR ESTADO DE EEUU
df["estado_provincia"].value_counts()

ANÁLISIS DE GENERO VE CADA MÁS CADA PAÍS
generos_paises = df.groupby("país")["genre_primary"].describe() preferencias_paises = generos_paises[["top"]].reset_index() preferencias_paises.columns = ["País", "Genero Favorito"] preferencias_paises

SEGMENTACIÓN DEL NUESTRO ANÁLISIS ENTRE LAS CIUDADES Y ESTADOS DEL OESTE Y EL ESTE
SEGMENTACIÓN DEL ESTE
provincias_orientales_estados = [ 'Carolina del Norte', 'Tennessee', 'Indiana', 'Michigan', 'Florida', 'Illinois', 'Georgia', 'Massachusetts', 'Maryland', 'Nueva York', 'Nueva Jersey', 'Ohio', 'Virginia', 'Pensilvania', 'Nueva Escocia', 'Quebec', 'Isla del Príncipe Eduardo', 'Terranova y Labrador', 'Nuevo Brunswick', 'Wisconsin', 'Ontario' ]

SEGMENTACIÓN DEL OESTE
estados_provincias_occidentales = [ 'Texas', 'California', 'Missouri', 'Washington', 'Arizona', 'Manitoba', 'Alberta', 'Columbia Británica', 'Saskatchewan' ]

Creamos DataFrame para estados del Este
df_eastern = df[df['state_province'].isin(eastern_provinces_states)]

2. El cambio está aquí: usamos df_eastern en lugar de df_western
resumen_generos = df_eastern.groupby('state_province')['genre_primary'].describe()

3. Extraemos el valor más frecuente ('top') o el genero más visto
preferencias_este = resumen_generos[['top']].reset_index()

4. Renombramos para que sea auto-explicativo
preferencias_este.columns = ['Estado / Provincia', 'Género Favorito']

preferencias_este

Creamos DataFrame para estados del Oeste
Filtramos primero (ojo con no cruzar las variables aquí)
df_occidental = df[df['estado_provincia'].isin(estados_provincias_occidentales)]

Sacamos el conteo del oeste
top3_oeste = df_western['genre_primary'].value_counts().head(3).reset_index()

Renombramos columnas
top3_oeste.columns = ['Género (Oeste)', 'Cantidad de Visualizaciones']

print("\n--- TOP 3 GÉNEROS EN EL OESTE ---") display(top3_oeste)

SEGMENTACIÓN GEOGRÁFICA DEL ANÁLISIS
