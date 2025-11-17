# Práctica Big Data: Hadoop ↔ Elasticsearch ↔ Kibana 

Este repositorio documenta, de forma sencilla, cómo conecté un clúster de Hadoop/Hive con un servidor de Elasticsearch y visualicé los datos en Kibana. No es una guía profesional ni de producción; es un resumen didáctico de lo que se hizo en una práctica de Bootcamp para entender los componentes y cómo se relacionan.

---

## Objetivo de la práctica

- Preparar un clúster con Hadoop y Hive.
- Desplegar un servidor de Elasticsearch de manera independiente.
- Conectar Hive con Elasticsearch mediante el conector oficial (ES-Hadoop).
- Enviar datos a Elasticsearch y comprobarlos desde el clúster.
- Crear un dashboard sencillo en Kibana con esos datos.
- Dejar evidencias y notas para que se pueda revisar el trabajo.

---

## Qué herramientas utilicé

- **Google Cloud Dataproc** para tener Hadoop y Hive listos en un clúster administrado.
- **Elasticsearch 8.x** como motor de búsqueda y analítica de documentos JSON.
- **Kibana 8.x** como interfaz web para visualizar y explorar los índices de Elasticsearch.
- **Conector ES‑Hadoop** (elasticsearch‑hadoop) para que Hive pueda leer/escribir en Elasticsearch.
- **Almacenamiento en Google Cloud Storage (bucket)** para intercambiar archivos de soporte.
- **Reglas de firewall y/o túneles SSH** para permitir que los distintos componentes se comuniquen de forma controlada.
- Utilidades de sistema para administración básica (por ejemplo, cliente de línea de comandos, herramientas de sistema y red).

---

## Arquitectura 

- **Máquina A: Clúster Dataproc (Hadoop/Hive).**
- **Máquina B: VM con Elasticsearch** (y Kibana en la misma VM para simplificar).

La idea es que Hive, desde el clúster, pueda enviar y/o consultar datos en un índice de Elasticsearch. Kibana se conecta a Elasticsearch para crear gráficos y paneles. La comunicación puede ser por red interna (misma VPC) o a través de IP pública con reglas de firewall restringidas.

---

## Lo que hice, paso a paso 

1. **Clúster Dataproc**  
   - Creé un clúster con Hive operativo.  
   - Subí al clúster las bibliotecas necesarias del conector ES‑Hadoop.

2. **Servidor de Elasticsearch**  
   - Desplegué una VM Linux e instalé Elasticsearch 8.x.  
   - Lo configuré en modo de laboratorio (instancia única, sin autenticación avanzada).  
   - Validé que el servicio estuviera activo y accesible desde el clúster.

3. **Conexión Hive ↔ Elasticsearch**  
   - Añadí en la configuración de Hive las propiedades para señalar el servidor de Elasticsearch, el puerto y la ruta de las bibliotecas del conector.  
   - Reinicié los servicios de Hive para que tomaran la nueva configuración.

4. **Carga y verificación de datos**  
   - Preparé unos documentos de ejemplo y los envié al índice de Elasticsearch.  
   - Consulté el índice desde el clúster para comprobar que los datos estaban disponibles.

5. **Kibana (dashboard sencillo)**  
   - Accedí a Kibana y registré una vista de datos sobre el índice utilizado.  
   - Creé visualizaciones simples (ejemplo: gráfico de dona, barras o métrica) y las añadí a un dashboard.  
   - Ajusté filtros y presentación para que fuese fácil de leer.

---

## Consideraciones de red y seguridad (versión práctica)

- Si el clúster y la VM están en **la misma red**, es cómodo usar direcciones internas y evitar exponer servicios al exterior.  
- Si se usan **IPs públicas**, hay que abrir únicamente los puertos necesarios y solo para las direcciones de origen que correspondan (por ejemplo, la IP del máster del clúster y la IP del equipo del alumno).  
- Para fines didácticos, la práctica se realizó con una configuración de seguridad básica. En entornos reales se recomienda habilitar autenticación, cifrado y gestionar certificados.

---

## Evidencias y entregables sugeridos

- Captura del clúster con las bibliotecas del conector presentes.  
- Captura de la configuración de Elasticsearch (archivo principal de configuración desde la VM).  
- Captura de la configuración de Hive con las propiedades del conector.  
- Captura de la consulta al índice creada desde el clúster (para ver los documentos insertados).  
- Captura del dashboard de Kibana con las visualizaciones realizadas.

---

## Qué se aprendió 

- Cómo se integran herramientas del ecosistema Big Data con un motor de búsqueda como Elasticsearch.  
- La importancia de **la red** (VPC, puertos, reglas) para que los componentes se comuniquen.  
- Dónde se configura cada pieza: Hive, Elasticsearch y Kibana.  
- Cómo validar de forma incremental: primero el servicio, luego la conectividad, después los datos, y finalmente la visualización.

---

## Créditos y agradecimientos

- Práctica realizada como parte de un módulo de Big Data Architecture en un Bootcamp.  
- Gracias a la documentación oficial de cada herramienta y a las guías del curso como referencia.

---

Si alguien revisa este repositorio y detecta oportunidades de mejora, ¡son bienvenidas! La intención es aprender haciendo y dejar constancia del flujo completo de **Hadoop/Hive → Elasticsearch → Kibana** de forma clara y accesible.
