# Laboratorio 2:

## Prerequisitos de Software requerido, Antivirus e Imagen a emplearse en el Laboratorio
1. Tener instalado el software siguiente:
1.a Autopsy https://www.autopsy.com/download/
1.b RegRipper https://github.com/keydet89/RegRipper3.0

2. Desactivar su antivirus
3. Disponer de 13GB de espacio libre en Disco Duro
4. Descargar la imagen forense a utilizarse en el caso: https://drive.google.com/file/d/1VBXP8JRsUyaJgUKbIWmcN3bJ4bgyg9Yb/view?usp=sharing
La Clave: Un1versid4d2022@105ER

## Caso de Estudio

Como parte de una práctica comercial normal, la seguridad de Walmart recibe alertas de cupones falsos de la Coupon Information Corporation. En el último mes, la seguridad de Walmart ha recibido información específica información sobre cupones fraudulentos que se pasan en su tienda. Con la información recibida se llevó a cabo una investigación interna utilizando imágenes de videovigilancia en un esfuerzo por identificar a los clientes que se dedican a esta actividad.

Uno de los sospechosos era un adulto blanco, desconocido, de aproximadamente 28 años, pelo castaño, 1.70 m, 90 kilos, sin vello facial y sin tatuajes visibles. Una fotografía de este sospechoso se hizo circular entre los empleados de la tienda.

El 22 de diciembre de 2013, Craig Tucker fue detenido por la seguridad de Walmart ya que coincidía con la descripción y acababa de pasar 2 cupones fraudulentos de bebidas energéticas Monster y Arizona Ice Tea mientras pagaba otros artículos.

La seguridad de Walmart se puso en contacto con el Departamento de Policía de Santa Mónica para detener y procesar a Tucker por robo.

El oficial Smith del Departamento de Policía de Santa Mónica entrevistó a Tucker y éste negó saber que los cupones eran fraudulentos. Tucker afirmó haber recibido los cupones después de completar una encuesta en línea para los estudiantes de Santa Mónica Community College.

Aunque Tucker dio su consentimiento para el registro de su ordenador personal, se obtuvo una orden de registro para registrar su ordenador en busca de pruebas, ya que puede ser un instrumento para cometer un delito.

En ese sentido, como perito te han dado una imagen forense de su disco duro. Basándose en su revisión de la orden de registro, usted está autorizado a buscar cualquier información o comunicación asociada a la creación, descarga, distribución y posesión de cupones fraudulentos para consumidores.

Craig fue atrapado con los siguientes cupones:

![image](https://user-images.githubusercontent.com/50930193/177678568-8e5233e3-5cc2-4dfc-88c8-7ed5d1c4cd9b.png)

![image](https://user-images.githubusercontent.com/50930193/177678639-6f608711-b335-4cfe-9f55-51f95393194c.png)

Ud. es el perito que ha sido asignado al caso y se te ha proporcionado la imagen de la evidencia en el archivo **ImagenForense.zip** para que Ud. efectúe el análisis del caso.

Ud. Deberá responder las preguntas siguientes:

## Preguntas

1.	¿Cuál es el hash SHA1 de la imagen? 
2.	¿Qué tipo de sistema operativo fue usado en la computadora?
3.	¿Cuándo fue realizada la fecha de instalación?
5.	¿Quién es el propietario registrado?
6.	¿Cuál es el nombre de la computadora?
7.	¿Cuáles son los usuarios de la computadora?, pueden ir a la colmena SAM bajo la siguiente subclave: SAM-Dominios-Cuenta-Usuarios
8.	¿Cual es el Rid del Usuario de Tucker? Ejemplo de RID de un usuario Rberrospi no precisamente del caso es el siguiente
```
Username        : Rberrospi [501]
Full Name       : 
User Comment    : Built-in account for guest access to the computer/domain
Account Type    : Default Guest Acct
Account Created : 2022-12-17 14:11:30Z
Name            :  
Last Login Date : Never
Pwd Reset Date  : Never
Pwd Fail Date   : Never
Login Count     : 0
Embedded RID    : 501
  --> Password does not expire
  --> Account Disabled
  --> Password not required
  --> Normal user account
```

9.	¿Cuándo fue la última fecha que la computadora fue apagada?
10.	¿Cuántas cuentas están grabadas (número total)?
11.	¿Cuál es el nombre del usuario quien utiliza mayormente la computadora?
12.	¿Quién fue el último usuario que se logueo en la computadora?
13. ¿En qué fecha y hora se creó y modificó AWESOME COUPONS.docx?
14. ¿Ha abierto Tucker alguna vez el archivo 6CommandmentsofCouponMaking.docx? Si es así, ¿cuándo fue la ÚLTIMA vez que lo abrió?
abrió?
15. ¿Dónde se encontraba el archivo "underage daughter R@ygold.wmv" cuando se abrió?
16. ¿Fue borrado el archivo "underage daughter R@ygold.wmv"? ¿Se puede recuperar?
17. ¿Cuándo se borró el archivo Underage_lolita_r@ygold_001.jpg?
18. ¿Ha abierto Tucker alguna vez el archivo "6CommandmentsofCouponMaking.docx"? Si es así, ¿cuándo fue la última vez que lo abrió?
abrió?
19. ¿Cuándo se envió el Re: Correo electrónico sobre la creación de cupones enviado a Craig? ¿Cuáles eran los nombres de los archivos adjuntos?
20. ¿Qué búsquedas en Google realizó Craig relacionadas con los cupones?

Bonus: ¿Dónde descargó Craig ALL COUPONS.rar?

