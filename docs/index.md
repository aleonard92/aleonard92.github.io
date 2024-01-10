# **Wiki de Lendbot BCI**

Bienvenido a la documentación de **Lendbot BCI**, aqui se dispone de la doumentación tanto del front como del backend.

## Widget
Esta es la herramieta principal de **BCI** mediante el cual se crean las cuentas del banco, la cual consta de 3 flujos principales, validación, firma y creación de cuenta.

### Instalación
Clonar el repositorio [bci-pyme-pj-widget](https://us-west-2.console.aws.amazon.com/codesuite/codecommit/repositories/bci-pyme-pj-widget/browse?region=us-west-2).

### Guia para los desarrolladores
En la primera pantalla del widget encontramos la funcionalidad Google Recaptcha la cual permite coomporbar si el usuario es un bot o una persona real

![fotoWidget](assests\widget.jpeg)

Para realizar esta funcionalidad se uso la libreria _react-google-recaptcha-v3_, la cual para su uso requiere una cuenta de google donde configuramos la que sitio vamos a controlar, la versión de recaptcha que se usará, entre otras configuraciones.
La cuenta usada para configurar el recaptcha del widget es:

> Cuenta:
>
>user: dm-bci@datamart.co
>
>passw: dmDM<dQhhNXN3hX%

El funcionamiento es sencillo se envuelve toda la aplicacion dentro de un contexto que te brinda la librería 

```js
<GoogleReCaptchaProvider
    reCaptchaKey={siteKey}
    scriptProps={{
      async: false,
      defer: false,
      appendTo: 'head',
      nonce: undefined,
    }}
    container={{
      // optional to render inside custom element
      element: 'base-component',
      parameters: {
        badge: 'bottomleft', // optional, default undefined
      },
    }}
    >
      <App />
    </GoogleReCaptchaProvider>
```
Luego en el formulario donde quieres validar si el usuario es una persona usas la funcionalidad executeRecaptcha de la siguiente manera:

```js
 useEffect(() => {
    if (executeRecaptcha)
      executeRecaptcha('enquiryFormSubmit').then((gReCaptchaToken) => {
        if (matches('enteringRut')) {
          send(new VerifyRecaptcha(gReCaptchaToken));
        }
      });
  }, [executeRecaptcha]);
```

