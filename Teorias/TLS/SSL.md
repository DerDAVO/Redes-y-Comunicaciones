Aquí tienes la explicación del **handshake** en **TLS/SSL** en formato **Markdown**:

---

# Handshake en TLS/SSL

El **handshake** (apretón de manos) es el proceso inicial mediante el cual el cliente (como un navegador web) y el servidor acuerdan los parámetros para establecer una conexión segura usando el protocolo **TLS/SSL**. Este proceso es esencial para garantizar que ambas partes se autentiquen mutuamente, acuerden los algoritmos de cifrado y generen las claves que se usarán para encriptar los datos durante la sesión.

## Pasos del **handshake** en TLS/SSL:

1. **Cliente envía el mensaje "ClientHello"**:
   - El cliente (User Agent, como un navegador) envía un mensaje llamado **ClientHello** al servidor, que contiene:
     - **Versión de TLS/SSL** que el cliente soporta.
     - **Lista de algoritmos de cifrado** (cipher suites) que el cliente puede utilizar.
     - **Datos aleatorios** generados por el cliente (que luego se usarán para generar claves de sesión).
     - Opcionalmente, una lista de **extensiones** (como compatibilidad con ciertas características avanzadas de seguridad).

2. **Servidor responde con "ServerHello"**:
   - El servidor responde con un mensaje **ServerHello**, que contiene:
     - La **versión de TLS/SSL** que se usará (negociada entre las opciones del cliente y las que soporta el servidor).
     - El **algoritmo de cifrado** seleccionado (de la lista proporcionada por el cliente).
     - **Datos aleatorios** generados por el servidor.
   
3. **Servidor envía su certificado**:
   - El servidor envía su **certificado digital** al cliente. Este certificado contiene la **clave pública** del servidor y es emitido por una **autoridad certificadora (CA)** de confianza.
   - El cliente verifica la validez del certificado asegurándose de que:
     - El certificado fue emitido por una autoridad confiable.
     - El certificado no ha expirado.
     - El nombre del servidor coincide con el que aparece en el certificado.
     - El certificado no ha sido revocado.

4. **(Opcional) Solicitud de certificado del cliente**:
   - En algunos casos (cuando se requiere una autenticación mutua), el servidor puede solicitar al cliente que proporcione su propio certificado para verificar su identidad.

5. **Cliente genera y envía el "PreMaster Secret"**:
   - El cliente genera un valor secreto llamado **PreMaster Secret**.
   - Este valor se encripta utilizando la **clave pública** del servidor (obtenida del certificado) y se envía al servidor. Solo el servidor, que posee la **clave privada** correspondiente, puede desencriptar el PreMaster Secret.

6. **Ambas partes generan la clave de sesión**:
   - Tanto el cliente como el servidor usan el **PreMaster Secret** (generado por el cliente) y los datos aleatorios intercambiados previamente (del ClientHello y ServerHello) para generar una **clave de sesión**. Esta clave de sesión será utilizada para encriptar y desencriptar todos los datos que se intercambien durante la conexión.
   
7. **Cliente envía el mensaje "ChangeCipherSpec"**:
   - El cliente envía un mensaje llamado **ChangeCipherSpec**, indicando que a partir de ese momento utilizará la clave de sesión y los algoritmos de cifrado acordados para proteger la comunicación.
   - También envía un mensaje **"Finished"**, que está encriptado utilizando la nueva clave de sesión. Este mensaje sirve para verificar que el cliente y el servidor han completado con éxito el handshake.

8. **Servidor responde con su "ChangeCipherSpec" y "Finished"**:
   - El servidor también envía un mensaje **ChangeCipherSpec**, indicando que ahora comenzará a usar la clave de sesión para encriptar su lado de la comunicación.
   - El servidor envía su propio mensaje **"Finished"**, también encriptado con la clave de sesión.

## Resultado del handshake:

- Si ambos mensajes "Finished" son verificados correctamente, la conexión segura se ha establecido exitosamente.
- A partir de este momento, toda la comunicación entre el cliente y el servidor estará **encriptada** utilizando la clave de sesión generada durante el handshake.

## Resumen visual del handshake en **TLS**:

1. **ClientHello** → Cliente envía versión de TLS, algoritmos de cifrado y datos aleatorios.
2. **ServerHello** → Servidor responde con versión de TLS, algoritmo de cifrado seleccionado y sus propios datos aleatorios.
3. **Servidor envía su certificado** → Incluye la clave pública para la encriptación.
4. **Cliente verifica el certificado** → Confirma que es válido y de confianza.
5. **PreMaster Secret** → Cliente genera un secreto que cifra con la clave pública del servidor.
6. **Claves de sesión** → Tanto el cliente como el servidor usan los datos intercambiados y el PreMaster Secret para generar la clave de sesión.
7. **ChangeCipherSpec** → Cliente y servidor activan el cifrado utilizando la clave de sesión.
8. **Finished** → Ambos intercambian mensajes encriptados que verifican que el handshake fue exitoso.

## Seguridad y autenticación:

- El handshake garantiza que el servidor es quien dice ser gracias a su certificado digital. Si el cliente también envía su certificado (en autenticación mutua), ambas partes pueden autenticarse.
- El uso de la clave de sesión para encriptar los datos asegura que la información intercambiada durante la conexión esté protegida de interceptaciones y ataques de tipo **man-in-the-middle**.

## Resumen:

El **handshake de TLS/SSL** es el proceso mediante el cual cliente y servidor acuerdan los algoritmos de cifrado, intercambian certificados para autenticarse mutuamente y generan una clave de sesión compartida que se utilizará para encriptar los datos durante la conexión.

---

Este formato usa elementos básicos de **Markdown** para estructurar la explicación, como títulos, listas numeradas y resaltados en negrita.