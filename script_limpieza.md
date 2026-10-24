let
    // Paso 1: Carga el archivo CSV original provisto por el sistema
    Origen = Csv.Document(File.Contents("Z:\table(1).csv"),[Delimiter=",", Columns=5, Encoding=65001, QuoteStyle=QuoteStyle.None]),
    
    // Promueve la primera fila como cabecera de las columnas
    #"Encabezados promovidos" = Table.PromoteHeaders(Origen, [PromoteAllScalars=true]),
    
    // Paso 2: Eliminar espacios al inicio y al final en nombre_producto
    LimpiarEspacios = Table.TransformColumns(#"Encabezados promovidos", {{"nombre_producto", Text.Trim, type text}}),

    // Paso 3: Estandarizar la columna categoria a Title Case (Computación, Accesorios, etc.)
    EstandarizarCategoria = Table.TransformColumns(LimpiarEspacios, {{"categoria", Text.Proper, type text}}),

    // Paso 4: Filtrar y eliminar registros cuya categoría sea "Prueba"
    EliminarPruebas = Table.SelectRows(EstandarizarCategoria, each [categoria] <> "Prueba"),

    // Paso 5: Asignar y corregir los tipos de datos correctos para cada columna
    TiparColumnas = Table.TransformColumnTypes(EliminarPruebas, {
        {"id_venta", Int64.Type},
        {"nombre_producto", type text},
        {"categoria", type text},
        {"precio", type number},
        {"fecha_venta", type date}
    })
in
    TiparColumnas

