SUBIR A REPOSITORIO

```
git init
```

```
git add .
```

```
git commit -m "comentario"
```

```
git branch -M main
```

```
git remote add origin enlace
```

```
git push -u origin main
```

SOLUCIÓN PULL REQUEST 
```
git checkout rama
```

```
git branch main rama -f
```

```
git checkout main
```

```
git push origin main -f
```

SOLUCIÓN DE ERRORES MASTER --> MAIN

```
git fetch origin main:tmp
```

```
git rebase tmp
```

```
async function obtenerProductos() {
    const requestOptions = {
        method: "GET",
        redirect: "follow"
    };

    try {
        const response = await fetch("http://localhost:8080/api/productos/todos", requestOptions);
        const productos = await response.json();
        listProductos = productos;

        // Realizar todas las solicitudes de predicción en paralelo
        const predicciones = await Promise.all(
            productos.map(producto =>
                fetch(`http://localhost:8080/api/prediccion/valor_venta?precio=${producto.precioFinal}`, requestOptions)
                    .then(res => res.json())
                    .catch(() => null) // Manejar errores individuales
            )
        );

        // Construir el HTML
        let galleryHTML = '';
        let tBodyHTML = '';

        productos.forEach((producto, index) => {
            const xSells = predicciones[index] ? parseFloat(predicciones[index]).toFixed(2) : "N/A";
            const precioFixed = new Intl.NumberFormat("es-CO", { style: "currency", currency: "COP", maximumFractionDigits: 0 }).format(producto.precioFinal);

            galleryHTML += `
                <clothe-card 
                    urlImg="${producto.imgPrenda}"
                    nombrePrenda="${producto.nombre}"
                    descripcionPrenda="${producto.descripcion}"
                    color="${producto.color}"
                    talla="${producto.talla}"
                    stock="${producto.stock}"
                    precio="${precioFixed}"
                    xSells="${xSells}">
                </clothe-card>
            `;

            tBodyHTML += `
                <tr class="odd:bg-white even:bg-gray-50 border-b dark:bg-gray-800 whitespace-nowrap">
                    <th scope="row" class="flex items-center px-5 py-2 text-gray-900 dark:text-gray-300">
                        <img class="w-9 h-9 rounded-full object-contain" src="${producto.imgPrenda}" alt="${producto.nombre}">
                        <div class="ps-1 whitespace-nowrap">
                            <div class="text-base font-semibold">${producto.nombre}</div>
                            <div class="font-normal text-gray-500 dark:text-gray-300"><strong>Talla: </strong>${producto.talla} | <strong>Ventas esperadas: </strong>${xSells}</div>
                        </div> 
                    </th>
                    <td class="px-5 py-2 dark:text-gray-50">${precioFixed}</td>
                    <td class="px-5 py-2 dark:text-gray-300">${producto.stock}</td>
                    <td class="px-5 py-2 dark:text-gray-300">${producto.tipo}</td>
                    <td class="px-5 py-2 dark:text-gray-300">${producto.color}</td>
                    <td class="px-5 py-2 text-sm dark:text-gray-300 max-w-xs break-words whitespace-normal">${producto.descripcion}</td>
                    <td class="px-5 py-2 dark:text-gray-300">${producto.proveedor.nombreEmpresa}</td>
                    <td class="px-5 py-2 -ml-5 flex space-x-2">
                        <i class="fa-solid fa-pen-circle text-green-600 dark:text-green-400 text-3xl cursor-pointer" onclick="editarProducto('modalProduct', ${producto.id})"></i>
                        <i class="fa-solid fa-circle-trash text-red-600 dark:text-red-400 text-3xl cursor-pointer" onclick="confirmarEliminacion('deleteModal',${producto.id})"></i>
                    </td>
                </tr>
            `;
        });

        // Actualizar el DOM una sola vez
        gallery.innerHTML = galleryHTML;
        tBody.innerHTML = tBodyHTML;
    } catch (error) {
        console.error(error);
    }
}

```

```
git push -u origin main
```

