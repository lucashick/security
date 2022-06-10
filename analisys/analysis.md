# Análisis Dinámico de la Aplicación
## Autenticación
- [ ] Proceso de registración de usuarios
- [ ] Proceso de password reset  

     Password reset tokens (caducidad/reutilización)
- [ ] Bloqueo de cuenta por reintentos fallidos
- [ ] Política de Passwords
- [ ] Update de información de cuenta sin pedir contraseña
- [ ] Claves por defecto o de fácil adivinación
- [ ] Enumeración de usuarios
- [ ] Autenticación por HTTP
- [ ] Bypass de autenticación
- [ ] Identificar canales de autenticación alternativos débiles (encontrar el mecanismo principal e identificar otros mecanismos secundarios ej: App Mobile, Call center, SSO)
## Autorización
- [ ] Testing Directory traversal/file include
- [ ] Acceso a funcionalidades/datos no disponibles para el rol actual (escalamiento de privilegios, horizontal y vertical)  

     Ejemplo: Acceso a funcionalidades de administración desde usuario sin privilegios (crear, borrar, modifcar usuarios...)
- [ ] IDORs  

     Ejemplo: La siguiente URL traería nuestra información personal: target.com/perfil?idUser=123 Cambiar por target.com/perfil?idUser=124 Trae información? Deberíamos tener acceso a 124?
- [ ] Implementación de OAuth 2.0   
## Sesión
- [ ] No validación de cookie
- [ ] No seteo de nueva cookie de sesión (session fixation)
- [ ] Cookie fácilmente reversible (base64/Hash ID)
- [ ] Seteo de cabeceras de seguridad (secure/HttpOnly)
- [ ] Testing for Cross Site Request Forgery 

     Eliminar token (parámetro y header) · Forjar un token propio · Usar un segundo parámetro · CSRF idéntico · Cambiar POST por GET 
 
     Funcionalidades donde conviene testear: · Agregar/Subir archivo · Cambio de Email · Eliminación de archivos · Cambio de Password · Transferencia de dinero · Edición de perfil
- [ ] Logout  
     Cierra la sesión realmente?
- [ ] Session timeout  
     La sesión caduca luego de un tiempo prudente?
- [ ] JWT  
      Chequeo de firma Chequeo de claims (especialmente aud "salto de entorno") Algoritmo de firmado Información sensible dentro del token

     - [c-jwt-cracker](https://github.com/brendan-rius/c-jwt-cracker)

          Fuerza bruta, ejemplo: ./jwtcrack eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.cAOIAifu3fykvhkHpbuhbvtH807-Z2rI1FS3vX1XMjE

     - [jwt_tool](https://github.com/ticarpi/jwt_tool)

          Chequea varias vulns, crackeo por diccionario Ejemplo: python3 jwt_tool.py

     - [JWT2Jhon](https://raw.githubusercontent.com/Sjord/jwtcrack/master/jwt2john.py)

          Para convertir los JWT a formato crackeable por John python3 jwt2john.py

          Ejecutar John: ./john /tmp/token.txt —wordlist=wordlist.txt
