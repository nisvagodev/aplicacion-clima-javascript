# Aplicación de Clima JavaScript

Link para ver el resultado: [APLICACION DE CLIMA TRABAJO FINALIZADO](https://clima-javascript-project.netlify.app/)

![Captura de pantalla del proyecto de Clima](https://github.com/nisvagodev/aplicacion-clima-javascript/blob/main/assets/img/captura-de-pantalla.PNG?raw=true)

La aplicación muestra datos en tiempo real del clima de una ciudad específica utilizando la API de OpenWeatherMap.

## Estructura del código

A continuación se muestra el código JavaScript necesario para realizar la solicitud a la API de OpenWeatherMap y mostrar los datos del clima en la aplicación.

El código anterior consta de dos funciones principales: `fetchDatosClima(ciudad)` y `mostrarDatosClima(data)`. Aquí está cómo funciona cada una:

1.  `fetchDatosClima(ciudad)`: Esta función se encarga de hacer una solicitud a la API de OpenWeatherMap para obtener los datos del clima de la ciudad especificada. Recibe el nombre de la ciudad como parámetro. Utiliza la función `fetch()` para enviar una solicitud GET a la URL de la API, incluyendo la ciudad y la clave de API. Luego, convierte la respuesta en formato JSON utilizando el método `json()`. Finalmente, llama a la función `mostrarDatosClima(data)` pasando los datos obtenidos como argumento.

    function fetchDatosClima(ciudad){
    fetch(`${urlBase}?q=${ciudad}&appid=${api_key}`)
    .then(data => data.json())
    .then(data => mostrarDatosClima(data))
    }

2.  `mostrarDatosClima(data)`: Esta función se encarga de mostrar los datos del clima en la página. Recibe los datos del clima en formato JSON como parámetro. Primero, obtiene las diferentes propiedades relevantes de los datos, como el nombre de la ciudad, el nombre del país, la temperatura, la humedad, la descripción y el icono del clima. Luego, crea elementos HTML apropiados, como encabezados y párrafos, y les asigna el contenido correspondiente utilizando la propiedad `textContent`. También crea un elemento de imagen para mostrar el icono del clima. Finalmente, agrega todos los elementos creados al elemento `<div>` con el ID "datosClima" en la página.

    function mostrarDatosClima(data){
    const divDatosClima = document.getElementById('datosClima')
    divDatosClima.innerHTML=''

        const ciudadNombre = data.name
        const paisNombre = data.sys.country
        const temperatura = data.main.temp
        const humedad = data.main.humidity
        const descripcion = data.weather[0].description
        const icono = data.weather[0].icon

        const ciudadTitulo = document.createElement('h2')
        ciudadTitulo.textContent = `${ciudadNombre}, ${paisNombre}`

        const temperaturaInfo = document.createElement('p')
        temperaturaInfo.textContent = `La temperatura es: ${Math.floor(temperatura-difKelvin)}ºC`

        const humedadInfo = document.createElement('p')
        humedadInfo.textContent = `La humedad es: ${humedad}%`

        const iconoInfo = document.createElement('img')
        iconoInfo.src= `https://openweathermap.org/img/wn/${icono}@2x.png`

        const descripcionInfo = document.createElement('p')
        descripcionInfo.textContent = `La descripción meteorológica es: ${descripcion}`

        divDatosClima.appendChild(ciudadTitulo)
        divDatosClima.appendChild(temperaturaInfo)
        divDatosClima.appendChild(humedadInfo)
        divDatosClima.appendChild(iconoInfo)
        divDatosClima.appendChild(descripcionInfo)

    }
