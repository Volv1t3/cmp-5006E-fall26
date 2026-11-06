# Resumen para el grupo

Traje el HW2 compartido por Santiago a `homework/hw2/tulcan/` y mantuve los tres
nombres. Organicé `attack/`, `defend/`, `duel/`, `honesty.md` y `AI_LOG.md` según
la estructura solicitada.

Agregué una prueba local de SQLi con tres bypasses de la misma clase y una
corrección propia usando parámetros. Esa prueba pasó: los tres bypasses evaden
el WAF; ninguno de los cuatro payloads filtra el canary con la corrección. El
WAF bloquea 2/26 entradas legítimas (7.69%). Esto corresponde a un laboratorio
SQLite adicional, no a una nueva ejecución de DVWA.

También corregí el notebook para que errores de conexión no cuenten como una
defensa exitosa. Los resultados originales están archivados y el notebook
modificado quedó sin salidas antiguas.

**Antes del PR:** falta ejecutar el notebook revisado en una máquina con DVWA,
Semgrep y Ollama para confirmar las dos variantes SQLi adicionales en Medium y
guardar resultados actuales. También documenté que el ground truth viene del
profesor y fue revisado después del duelo; no debemos decir que lo construimos
antes de las herramientas. En las dos corridas originales del LLM no hubo
alucinaciones observadas.

La rama compartida es `hw2-00329994` del fork `miatulcan/cmp-5006E-fall26`.
Este resumen está listo para copiar al chat del grupo; no se ha enviado a nadie
automáticamente.
