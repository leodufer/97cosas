---
layout: programador
title: El camino al mejor rendimiento está lleno de sucias bombas de código
overview: true
author: Kirk Pepperdine
translator: Espartaco Palma
original: http://programmer.97things.oreilly.com/wiki/index.php/The_Road_to_Performance_Is_Littered_with_Dirty_Code_Bombs
---

Más frecuentemente que nunca, la optimización de rendimiento en un sistema
requiere que alteres código. Cuando tenemos que modificar el código, cada
porción intrincadamente compleja o altamente acoplada es una sucia bomba de
código, en espera de descarrilar el esfuerzo. La primera víctima de código
sucio será tu agenda. Si el camino a seguir es suave, será fácil predecir
cuando acabará. Los encuentros inesperados con el código sucio harán que sea
muy difícil hacer una predicción cuerda.

Considera la situación donde encuentras un punto de ejecución complicado. El
curso normal de acción es reducir la fortaleza del algoritmo en cuestión.
Digamos que respondes con "3-4 horas" a un estimado que te pide el gerente. Si
aplicas el fix te darás cuenta rápidamente que has descompuesto una parte
dependiente. Debido a que las cosas están relacionadas, a menudo están
necesariamiente acopladas, estas descomposturas son esperadas y se cuenta con
ellas. Pero, ¿qué pasa si un arreglo en esa dependencia termina rompiéndose en
en otra parte dependiente? Por otro lado, entre más lejos está la dependencia
de su origen, menos probable es reconocerla como tal y tomarla en cuenta en
tu estimado. De repente tu estimado de 3-4 horas puede elevarse fácilmente a
3-4 semanas. Con frecuencia estos cambios en la agenda suceden 1 o 2 días,
todas al mismo tiempo. No es raro el ver refactorizaciones "rápidas" que
eventualmente toman varios meses en ser completadas. En esos casos, el daño
en la credibilidad y capital político del equipo responsable variará de severo
a terminal. Si tan sólo tuvieramos una herramienta para ayudarnos a
identificar y medir estos riesgos.

De hecho, tenemos varias maneras de medir y controlar el grado y profundidad de
acoplamiento y complejidad de nuestro código. Las métricas de software pueden
ser usadas para contar las apariciones de característica específicas en
nuestro código. Los valores de estos conteos se correlacionan con la calidad
del código. Dos de estas métricas que miden el acomplamento son las llamadas
_fan-in_ y _fan-out_. El _fan-out_ está definido como el número de clases
referenciadas, ya sea directa o indirectamente, para  una clase en particular.
Puedes pensar en esto como un recuento de todas las clases que deben ser
compliladas antes de que tu clase pueda ser compilada. El _fan-in_  es un
conteo de todas las clases que dependen de una clase en específico. Conociendo
el _fan-out_ y _fan-in_ podemos calcular un factor de inestabilidad usando
I = fo / (fi + fo). Conforme se aproxima a 0, el paquete se vuelve más
estable. En cuanto se aproxime a 1, el paquete se convierte en inestable. Los
paquetes que son estables son objetivos de bajo riesgo, mientras que los
paquetes inestables son más propensos a estar llenos de sucias bombas
de código. La meta de la refactorización es mover _I_ lo más cercano a 0.

Cuando usamos métricas debemos recordar que sólo son reglas empíricas.
Basándose puramente en las matemáticas puedes ver que el incremento de _fi_
sin cambiar _fo_ moverá _I_ mas cerca a 0. Sin embargo hay una desventaja en
tener el valor _fan-in_ alto, pues estas clases serán más difíciles de
modificar sin romper dependencias. Al no tener en cuenta el _fan-out_ no estás
reduciendo realmente el riesgo, por lo que debe aplicarse algún balance.

Una desventaja de las méticas de software es que el gran cantidad de números
que producen las herramientras asociadas pueden ser intimidantes para los no
iniciados. Dicho esto, las métricas de software pueden ser una poderosa
herramienta en nuestra lucha por un código limpio. Pueden ayudar a identificar
y eliminar las sucias bombas de código antes de que sean un serio riesgo al
ejercicio de optimización del rendimiento.

