.. title: Configuración para la printrbot simple
.. slug: configuracion-para-la-printrbot-simple
.. date: 2015-08-14 21:39:41 UTC-06:00
.. tags: 3dprint printrbot 
.. category: 
.. link: 
.. description: Gcode para inicio de impresión en la printrbot
.. type: text

Código:
-------

```
M104 S{TEMP0} ; set temperature
G21 ;metric values
G90 ;absolute positioning
M82 ;set extruder to absolute mode
M107 ;start with the fan off
G28 X0 Y0 ;move X/Y to min endstops
G28 Z0 ;move Z to min endstops
M109 S{TEMP0} ;wait on temperature line
G29 ; Auto bed levelling
G92 E0 ;zero the extruded length
G1 F{TRAVEL_SPEED} ;
```
