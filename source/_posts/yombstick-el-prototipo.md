---
title: "Yombstick: El prototipo"
date: 2013-01-29 14:18:34
tags: 
---
<p style="text-align: justify;">Por fin he resuelto el bug que tenía con el prototipo del Yombstick, un joystick USB customizado que estoy haciendo. Así que me he puesto a hacer un post, y me ha quedado bastante largo (30 fotos), porque me he liado a hacer cosas mientras lo escribía. Espero que no sea demasiado tostón.</p>
<p style="text-align: justify;">El bicho Lleva dos microcontroladores, un Atmega1284P para las entradas analógicas, botones, LEDs y demás, y un Atmega16U2 que <a href="http://yombo.org/2013/01/mi-primera-soldadura-smd/" target="_blank">conseguí soldar hace poco</a>, el cual se encargará de la comunicación USB y de aparecer ante el ordenador como un dispositivo HID con 8 ejes y 8 botones.</p>
<p style="text-align: justify;">De todas formas si veo que con 6 entradas analógicas me basta, usaré un Atmega328P en lugar de un 1284P, que son más baratos y además en este caso irá mejor porque es más pequeño y no hay mucho espacio en la base del joystick para circuitería. Dicho de paso, con un 16U2 y un Atmega328P, el circuito sería análogo a una placa Arduino Uno.</p>
<p style="text-align: justify;">En esta foto se ve la primera prueba en que funcionó el 16U2 como joystick:</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/1-PrimeraPruebaYombstick.jpg"><img class="aligncenter size-large wp-image-326" alt="1 PrimeraPruebaYombstick" src="http://yombo.org/wp-content/uploads/2013/01/1-PrimeraPruebaYombstick-1024x576.jpg" width="625" height="351" /></a></p>
<p style="text-align: justify;">El joystick en sí será un <a href="http://www.soyntec.com/ky-es/item/78351" target="_blank">Soyntec Challenger 250</a>, un joystick USB inalámbrico (a 27 MHz) que ya no funcionaba y me cedió mi amigo Álex.</p>
<p style="text-align: justify;">El Yombstick tendrá muchas características notables. En primer lugar, los valores de los ejes, en vez de ser números enteros de 8 bits (con signo, en complemento a 2) como en la mayoría de joysticks comerciales –con un rango de -128 a +127, que se considera suficiente–, serán de 16 bits con el mismo formato, con un rango de -32768 a +32767.</p>
<p style="text-align: justify;">En segundo lugar, le voy a poner un <em>hat</em> al joystick que será analógico, no como los de la mayoría de joysticks, que son simplemente cuatro pulsadores. Para ello usaré medio mando de una conocida consola, o sea una de las palancas con sus dos potenciómetros. El valor del joystick pequeño se sumará al del grande en una proporción de 0.12, lo que servirá en los movimientos de precisión. Y con los 16 bits de resolución supongo que dará buenos resultados.</p>
<p style="text-align: justify;">Lo del valor exacto de 0.12 es porque coincide con lo que suele ser la zona muerta considerada por el S.O. La zona muerta es la posición cercana a la central del joystick, y el S.O. pone valores a 0 por software en esa zona para evitar efectos mecánicos del joystick. A mí me interesa quitar la zona muerta y que la precisión sea buena en el centro. En Linux ya he conseguido quitar la zona muerta, veremos si podré hacer lo mismo en el Windows 7 en el que jugaré a <a href="http://elite.frontier.co.uk/" target="_blank">Elite: Dangerous</a>.</p>
En esta foto se ve el 16U2, aún sin su compañero el 1284P:
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/3-Nucleo-USBYombstick.jpg"><img alt="3 Nucleo USBYombstick" src="http://yombo.org/wp-content/uploads/2013/01/3-Nucleo-USBYombstick-1024x576.jpg" width="625" height="351" /></a></p>
<p style="text-align: justify;">En esta foto se puede ver un detalle del micro 16U2, que está soldado sobre un adaptador a DIP32, y los componentes para hacerlo funcionar: Cristal, condensadores, un LED con su resistencia, y en el conector USB, dos resistencias de 22 ohmios (azules) en las dos líneas de datos:</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/2-Detalle-16u2Yombstick.jpg"><img class="aligncenter size-large wp-image-327" alt="2 Detalle 16u2Yombstick" src="http://yombo.org/wp-content/uploads/2013/01/2-Detalle-16u2Yombstick-1024x576.jpg" width="625" height="351" /></a></p>
<p style="text-align: justify;">Aquí el prototipo ya completo. Los dos cables azules en el borde inferior de la placa blanca son el puerto serie (RX y TX) que une ambos microcontroladores. Por cierto aquí ya está conectado y funcionando (mirad los LEDs verde y rojo, ambos encendidos :-)</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/4-PrototipoYombstick.jpg"><img class="aligncenter  wp-image-329" alt="4 PrototipoYombstick" src="http://yombo.org/wp-content/uploads/2013/01/4-PrototipoYombstick.jpg" width="3776" height="2520" /></a></p>
<p style="text-align: justify;">Aquí una captura en la que se ve el programa <em>jstest-gtk</em> reconociendo el Yombstick con todos sus ejes y botones. Aquí el eje Y hacía además de <em>hat</em> de precisión para el eje X, sumado como he dicho tras ser multiplicado por 0.12:</p>
<a href="http://yombo.org/wp-content/uploads/2013/01/6-CapturaFuncionandoPrototipoYombstick.png"><img class="aligncenter size-full wp-image-331" alt="6 CapturaFuncionandoPrototipoYombstick" src="http://yombo.org/wp-content/uploads/2013/01/6-CapturaFuncionandoPrototipoYombstick.png" width="947" height="669" /></a>
<p style="text-align: justify;">Bueno, a partir de aquí voy a ir escribiendo el post y haciendo las fotos mientras desarmo el Soyntec. Empezamos:</p>
<a href="http://yombo.org/wp-content/uploads/2013/01/7-Soyntec-Challenger-250-Yombstick.jpg"><img class="aligncenter size-large wp-image-345" alt="7 Soyntec Challenger 250 Yombstick" src="http://yombo.org/wp-content/uploads/2013/01/7-Soyntec-Challenger-250-Yombstick-1024x683.jpg" width="625" height="416" /></a>
<p style="text-align: justify;">Empiezo por desarmar la palanca, que tiene unos tornillos que no había visto –y por tanto creía que sería mucho más difícil instalar botones y palancas customizados.<a href="http://yombo.org/wp-content/uploads/2013/01/8-Yombstick-desarmado-1.jpg"><img class="aligncenter size-large wp-image-346" alt="8 Yombstick desarmado 1" src="http://yombo.org/wp-content/uploads/2013/01/8-Yombstick-desarmado-1-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">Sale bastante fácil y se ven dos placas: una para los botones frontales y el <em>hat</em>, que no me interesan (el plástico del <em>hat</em> sí lo aprovecharé, pero no los botones de debajo)</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/9-Yombstick-desarmado-2.jpg"><img class="aligncenter size-large wp-image-353" alt="9 Yombstick desarmado 2" src="http://yombo.org/wp-content/uploads/2013/01/9-Yombstick-desarmado-2-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">La otra placa es de los botones laterales y el trigger (el gatillo o botón del índice). Ésta sí la debería aprovechar entera, pero los botones del pulgar están muy usados (no hacen ese ¡Click! de cuando nuevos), y como los pulsadores nuevos que tengo yo no coinciden en el patillaje con esos, tendré que hacer un duplicado de la placa y ponerla en el mismo sitio, con el mismo tornillo, ése que se ve encima de la placa en esta foto:</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/10-Yombstick-desarmado-4-placa-botones.jpg"><img class="aligncenter size-large wp-image-347" alt="10 Yombstick desarmado 4 placa botones" src="http://yombo.org/wp-content/uploads/2013/01/10-Yombstick-desarmado-4-placa-botones-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">Aquí se ven las palancas de la consola que tenía guardadas (creo que es de un mando viejo que me regaló mi hermano, no sé de dónde salió):</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/11-Yombstick-palanca-del-hat.jpg"><img class="aligncenter size-large wp-image-358" alt="11 Yombstick palanca del hat" src="http://yombo.org/wp-content/uploads/2013/01/11-Yombstick-palanca-del-hat-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">La piececita de plástico que se ve encima del mando y también en la siguiente foto es el <em>hat</em> original del Soyntec (del tipo pulsadores), que pegaré de alguna forma al mando blanco analógico.</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/12-Yombstick-palanca-del-hat-2.jpg"><img class="aligncenter size-large wp-image-359" alt="12 Yombstick palanca del hat 2" src="http://yombo.org/wp-content/uploads/2013/01/12-Yombstick-palanca-del-hat-2-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">Ahora vamos con la base. Bueno, en realidad ya la había desmontado otro día y ya le arranqué la electrónica original:</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/13-Yombstick-base-abierta.jpg"><img class="aligncenter size-large wp-image-360" alt="13 Yombstick base abierta" src="http://yombo.org/wp-content/uploads/2013/01/13-Yombstick-base-abierta-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">En este detalle se ven dos de los potenciómetros –parecen de buena calidad :-), el tercero es interno a la parte móvil y no se ve, pero sí los tres cables que vienen de él. Por otro lado está el acelerador o <em>throttle</em>, bien engrasadito:</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/14-Yombstick-base-abierta-detalle.jpg"><img class="aligncenter size-large wp-image-361" alt="14 Yombstick base abierta detalle" src="http://yombo.org/wp-content/uploads/2013/01/14-Yombstick-base-abierta-detalle-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">Ahora me pongo a desoldar la palanca:</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/15-Desoldando-palanca-analogica-Yombstick.jpg"><img class="aligncenter size-large wp-image-364" alt="15 Desoldando palanca analogica Yombstick" src="http://yombo.org/wp-content/uploads/2013/01/15-Desoldando-palanca-analogica-Yombstick-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">¡Conseguido! :-)</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/16-Desoldando-palanca-analogica-Yombstick-conseguido.jpg"><img class="aligncenter size-large wp-image-365" alt="16 Desoldando palanca analogica Yombstick conseguido" src="http://yombo.org/wp-content/uploads/2013/01/16-Desoldando-palanca-analogica-Yombstick-conseguido-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">El <em>hat</em> va perfecto. Como tiene un botón (se puede pulsar además de tener los dos ejes analógicos), se me ocurre que puedo usar ese botón para cambiar el eje Y del <em>hat </em>entre el eje Y y el Z del joystick, y mostrar el eje actual con un LED (bicolor quizá). El eje X del <em>hat</em> siempre va asociado al eje X del joystick.</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/17-Desoldando-palanca-analogica-Yombstick-detalle.jpg"><img class="aligncenter size-large wp-image-367" alt="17 Desoldando palanca analogica Yombstick detalle" src="http://yombo.org/wp-content/uploads/2013/01/17-Desoldando-palanca-analogica-Yombstick-detalle-1024x576.jpg" width="625" height="351" /></a></p>
<p style="text-align: justify;">Ahora voy a hacer la placa de los botones de los pulgares, con pulsadores y cables nuevos. Primero Hago un calco de la placa en otra de topos, cuidando que los botones coincidan con los agujeros (afortunadamente coinciden más o menos con la separación estándar):</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/18-Haciendo-la-placa-de-botones-de-los-pulgares-Yombstick.jpg"><img class="aligncenter size-large wp-image-369" alt="18 Haciendo la placa de botones de los pulgares Yombstick" src="http://yombo.org/wp-content/uploads/2013/01/18-Haciendo-la-placa-de-botones-de-los-pulgares-Yombstick-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/19-Haciendo-la-placa-de-botones-de-los-pulgares-2-Yombstick.jpg"><img class="aligncenter size-large wp-image-371" alt="19 Haciendo la placa de botones de los pulgares 2 Yombstick" src="http://yombo.org/wp-content/uploads/2013/01/19-Haciendo-la-placa-de-botones-de-los-pulgares-2-Yombstick-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">Aquí ya los botones soldados:</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/20-Haciendo-la-placa-de-botones-de-los-pulgares-3-Yombstick.jpg"><img class="aligncenter size-large wp-image-372" alt="20 Haciendo la placa de botones de los pulgares 3 Yombstick" src="http://yombo.org/wp-content/uploads/2013/01/20-Haciendo-la-placa-de-botones-de-los-pulgares-3-Yombstick-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">Aquí ya terminado y puesto en sus sitio. Los botones encajan bien, porque aunque son un poco más gruesos que los originales (menos de 1 mm), la placa es más delgada que la que había, y se ha compensado. Ahora suenan muy bien :-)</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/21-Haciendo-la-placa-de-botones-de-los-pulgares-4-Yombstick.jpg"><img class="aligncenter size-large wp-image-373" alt="21 Haciendo la placa de botones de los pulgares 4 Yombstick" src="http://yombo.org/wp-content/uploads/2013/01/21-Haciendo-la-placa-de-botones-de-los-pulgares-4-Yombstick-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">Aquí se ve el tornillo aguantando la placa. En el otro lado del joystick hay una pieza de plástico que aprisiona la placa y le da robustez a los botones.</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/22-Haciendo-la-placa-de-botones-de-los-pulgares-5-Yombstick.jpg"><img class="aligncenter size-large wp-image-374" alt="22 Haciendo la placa de botones de los pulgares 5 Yombstick" src="http://yombo.org/wp-content/uploads/2013/01/22-Haciendo-la-placa-de-botones-de-los-pulgares-5-Yombstick-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">Lo siguiente es desmontar la placa del <em>hat</em>:</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/23-Desmontando-el-hat-1-Yombstick.jpg"><img class="aligncenter size-large wp-image-378" alt="23 Desmontando el hat 1 Yombstick" src="http://yombo.org/wp-content/uploads/2013/01/23-Desmontando-el-hat-1-Yombstick-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">Tras desatornillar la placa de los botones queda una plaquita de plástico que se puede aprovechar para colocar los botones y LEDs, y también el nuevo <em>hat</em> analógico:</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/24-Desmontando-el-hat-2-Yombstick1.jpg"><img class="aligncenter size-large wp-image-379" alt="24 Desmontando el hat 2 Yombstick" src="http://yombo.org/wp-content/uploads/2013/01/24-Desmontando-el-hat-2-Yombstick1-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">Encaja bastante bien en el cuadrado, pero habrá que cortar toda la parte de fuera para que sobresalga lo suficiente. Eso será para la próxima sesión.</p>
De momento me he puesto a hacer los cables para los botones y los ejes que ya tengo: el gatillo, los dos del pulgar, los ejes X, Y y Z y el acelerador:
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/25-Cables-nuevos-Yombstick.jpg"><img class="aligncenter size-large wp-image-383" alt="25 Cables nuevos Yombstick" src="http://yombo.org/wp-content/uploads/2013/01/25-Cables-nuevos-Yombstick-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">Para pasar los cables por el centro del joystick lo he tenido que desmontar entero, es bastante intrincadillo...</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/26-Desmontando-el-interior-Yombstick.jpg"><img class="aligncenter size-large wp-image-384" alt="26 Desmontando el interior Yombstick" src="http://yombo.org/wp-content/uploads/2013/01/26-Desmontando-el-interior-Yombstick-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">Aquí con los cables ya pasados por la pieza interior:</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/27-Desmontando-el-interior-2-Yombstick.jpg"><img class="aligncenter size-large wp-image-385" alt="27 Desmontando el interior 2 Yombstick" src="http://yombo.org/wp-content/uploads/2013/01/27-Desmontando-el-interior-2-Yombstick-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">Montado el palo central en la base, con los cables ya saliendo:</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/28-Cables-sacados-Yombstick.jpg"><img class="aligncenter size-large wp-image-386" alt="28 Cables sacados Yombstick" src="http://yombo.org/wp-content/uploads/2013/01/28-Cables-sacados-Yombstick-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">Aquí con todos los conectores ya soldados (los potenciómetros ya tenían conectores pero no eran de paso estándar y los he sustituido todos):</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/29-Cables-sacados-2-Yombstick.jpg"><img class="aligncenter size-large wp-image-387" alt="29 Cables sacados 2 Yombstick" src="http://yombo.org/wp-content/uploads/2013/01/29-Cables-sacados-2-Yombstick-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">Y aquí finalmente el trasto ya listo para probar, puesto que si monto la base no me llegan los cables hacia el prototipo de la electrónica, y además éste no cabe en la base.</p>
<p style="text-align: justify;"><a href="http://yombo.org/wp-content/uploads/2013/01/30-Preparado-para-probar-30.jpg"><img class="aligncenter size-large wp-image-388" alt="30 Preparado para probar 30" src="http://yombo.org/wp-content/uploads/2013/01/30-Preparado-para-probar-30-1024x683.jpg" width="625" height="416" /></a></p>
<p style="text-align: justify;">Lo voy a dejar aquí por hoy. En la próxima entrega la prueba de lo que has visto hasta ahora, y en las siguientes, el circuito con esquemático y el <em>firmware</em>.</p>
<p style="text-align: justify;">Como comentario final, decir que me gusta bastante este joystick por lo modular y customizable que es.</p>
<p style="text-align: justify;">¡Hasta la próxima!</p>
<p style="text-align: justify;"></p>