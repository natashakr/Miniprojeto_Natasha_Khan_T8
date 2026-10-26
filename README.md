# Miniprojeto_Natasha_Khan_T8
# Objetivo
Leer, diagnosticar, limpiar y analizar una base de registros de compras de retail para extraer métricas de negocio confiables sobre volúmenes de ventas, categorías y perfiles de clientes, generando una versión tratada de los datos (varejo_limpo.csv).

# Origen de la Base y Unidad de Análisis
Origen: El archivo original (Base Varejo.csv) cuenta inicialmente con 830.000 filas y 14 columnas.   
Unidad de Análisis: Al comparar el total de registros (830.000) con los identificadores de compra únicos CO_ID (18.471), se concluyó que cada fila representa un artículo individual dentro de un pedido, y no una compra completa o un cliente único. 

# Columnas Utilizadas
CO_ID: Identificador único del pedido o compra.
CL_ID: Identificador único del cliente.
CL_FHL: Cantidad de hijos del cliente (utilizada para análisis estadístico numérico).
PR_CAT: Categoría del producto comprado.
PR_NOME: Nombre del producto comprado.

# Diagnóstico y Decisiones de Limpieza
Diagnóstico de Calidad: La inspección inicial reveló que no había valores nulos ni textos vacíos. Sin embargo, se identificaron columnas "fantasma" (Unnamed) generadas durante la lectura y 96.553 líneas exactamente duplicadas.   

Decisiones de Limpieza: Se eliminaron las columnas vacías (Unnamed). Se aplicaron los métodos .str.upper() y .str.strip() para estandarizar las columnas de texto (categoría y nombre) y evitar errores de agrupación.   Se eliminaron las duplicatas exactas (drop_duplicates()) tras verificar que eran redundancias de extracción, para no inflar artificialmente las métricas de volumen de ventas.  

# Funciones Creadas
Para garantizar la reutilización del código y organizar el pipeline, se crearon dos funciones:   
- tratar_texto(texto): Recibe un valor de texto y lo devuelve estandarizado (en mayúsculas y sin espacios adicionales).
- gerar_resumo(coluna): Recibe una serie numérica (en este caso, CL_FHL) y utiliza el método .describe() para retornar un diccionario o resumen con el conteo, media, mínimo y máximo.   

# Conclusiones de la Análisis
Reducción de la Base: Tras la limpieza justificada de duplicatas, la base analítica pasó de 830.000 a 733.447 registros confiables. 
Perfil del Cliente: El análisis de la columna CL_FHL (Cantidad de hijos) demostró que los clientes de esta base tienen en promedio 1.14 hijos.
Volumen por Categoría: El agrupamiento de ventas demostró que la categoría ALIMENTOS es la que concentra el mayor volumen, con 384.197 artículos vendidos.
Volumen por Producto: El producto más vendido de toda la tienda es el "PRESUNTO COZIDO", con 12.719 unidades registradas en las compras.Recomendación y LimitaciónRecomendación de Negocio: Se sugiere enfocar las estrategias de reposición de stock y promociones en la categoría "Alimentos", especialmente en los productos de alto volumen como el "Presunto Cozido". Además, se recomienda al equipo de ingeniería de datos revisar el origen de la extracción para solucionar el problema que genera las casi 100 mil filas duplicadas. 

# Limitación de la Análisis: 
Debido a que la base de datos suministrada no contenía información financiera (columnas de "Precio" o "Ingresos"), todo el análisis de rendimiento se basó exclusivamente en el volumen de artículos vendidos (conteo), lo que impide confirmar si la categoría más vendida es también la más rentable.  

