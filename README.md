\documentclass[11pt,a4paper]{article}

% =============== PAQUETES ===============
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage[spanish,es-tabla,es-nodecimaldot]{babel}
\usepackage[margin=2.5cm]{geometry}
\usepackage{graphicx}
\usepackage{xcolor}
\usepackage{colortbl}
\usepackage{tabularx}
\usepackage{longtable}
\usepackage{booktabs}
\usepackage{array}
\usepackage{enumitem}
\usepackage{titlesec}
\usepackage{fancyhdr}
\usepackage{hyperref}
\usepackage{setspace}
\usepackage{caption}
\usepackage{float}

% =============== COLORES ===============
\definecolor{azulprincipal}{RGB}{25,59,103}
\definecolor{azulsecundario}{RGB}{52,120,198}
\definecolor{grisclaro}{RGB}{240,240,240}
\definecolor{rojoriesgo}{RGB}{192,57,43}
\definecolor{naranjariesgo}{RGB}{230,126,34}
\definecolor{verdeok}{RGB}{39,174,96}

% =============== HIPERVÍNCULOS ===============
\hypersetup{
    colorlinks=true,
    linkcolor=azulprincipal,
    urlcolor=azulsecundario,
    citecolor=azulprincipal,
    pdftitle={Informe Consolidado - Arquitectura Empresarial - Cyber Nexus Grupo 7},
    pdfauthor={Grupo 7 - Cyber Nexus}
}

% =============== ENCABEZADO Y PIE DE PÁGINA ===============
\pagestyle{fancy}
\fancyhf{}
\fancyhead[L]{\small\textit{Arquitectura Empresarial}}
\fancyhead[R]{\small\textit{Cyber Nexus - Grupo 7}}
\fancyfoot[C]{\thepage}
\renewcommand{\headrulewidth}{0.4pt}
\renewcommand{\footrulewidth}{0.4pt}

% =============== FORMATO DE TÍTULOS ===============
\titleformat{\section}
    {\normalfont\Large\bfseries\color{azulprincipal}}
    {\thesection.}{0.5em}{}
\titleformat{\subsection}
    {\normalfont\large\bfseries\color{azulsecundario}}
    {\thesubsection}{0.5em}{}
\titleformat{\subsubsection}
    {\normalfont\normalsize\bfseries\color{azulsecundario}}
    {\thesubsubsection}{0.5em}{}

\setstretch{1.15}

% =============== INICIO DEL DOCUMENTO ===============
\begin{document}

% =============== PORTADA ===============
\begin{titlepage}
    \centering
    \vspace*{1cm}

    {\Large\textbf{UNIVERSIDAD DE LA SABANA}}\\[0.3cm]
    {\large Facultad de Ingeniería}\\[0.3cm]
    {\large Arquitectura Empresarial}\\[2cm]

    \rule{\linewidth}{0.5mm}\\[0.8cm]
    {\Huge\bfseries\color{azulprincipal} Informe Consolidado del Semestre}\\[0.5cm]
    {\LARGE\color{azulsecundario} Diagnóstico, Seguridad y Cumplimiento}\\[0.3cm]
    {\Large\itshape Talleres 4, 5 y 6 --- Proyecto Integrador}\\[0.3cm]
    \rule{\linewidth}{0.5mm}\\[2cm]

    {\large\textbf{Equipo de trabajo: Cyber Nexus --- Grupo 7}}\\[1.5cm]

    \begin{tabular}{rl}
        \textbf{Caso de estudio:} & Plataforma de gestión de propiedades y reservas \\
        \textbf{Cliente analizado:} & Sistema integrado con API de Airbnb \\
        \textbf{Repositorio:} & \href{https://github.com/Luis-Diaz-Cryo/ARQUITECTURA-EMP-Cyber-nexus-Grp-7}{GitHub --- Cyber Nexus Grp 7} \\
    \end{tabular}

    \vfill
    {\large \today}
\end{titlepage}

% =============== TABLA DE CONTENIDOS ===============
\tableofcontents
\newpage

% =============== INTRODUCCIÓN GENERAL ===============
\section{Introducción General}

El presente documento consolida el trabajo realizado por el grupo \textbf{Cyber Nexus --- Grupo 7} durante el semestre en la asignatura de \textbf{Arquitectura Empresarial}. A lo largo del curso se desarrollaron tres entregas sucesivas (Talleres 4, 5 y 6) que, en conjunto, constituyen un ejercicio integral de análisis arquitectónico, evaluación de seguridad y verificación de cumplimiento normativo sobre un mismo caso de estudio: una plataforma digital de gestión de propiedades y reservas que se integra con la API de Airbnb.

La decisión de unificar los tres informes en un único documento responde a una necesidad pedagógica y práctica: los tres talleres no son ejercicios aislados, sino capas complementarias de un mismo diagnóstico. El Taller 4 construye la base técnica al mapear la infraestructura; el Taller 5 añade la dimensión de ciberseguridad mediante el análisis STRIDE; y el Taller 6 cierra el ciclo con la verificación del cumplimiento normativo frente a la Ley 1581 de 2012 e ISO/IEC 27001. Solo cuando estas tres miradas se leen de forma conjunta se obtiene una visión completa del estado real del sistema y de las acciones que deben priorizarse.

Este informe está dirigido a dos audiencias principales. Por un lado, al \textbf{docente de la asignatura}, como evidencia consolidada del proceso, los hallazgos y las conclusiones alcanzadas durante el semestre. Por otro lado, a los \textbf{propios miembros del equipo}, como documento de referencia que recoge el conocimiento construido y que puede servir como base para futuros proyectos, certificaciones o intervenciones sobre sistemas con características similares.

\subsection{Contexto y Necesidad del Trabajo}

El caso de estudio seleccionado corresponde a un sistema real con múltiples frentes de análisis: infraestructura en la nube (AWS), arquitectura de microservicios, integraciones externas con plataformas de terceros, manejo de datos personales sensibles (clientes, reservas, pagos) y operación apoyada en herramientas manuales como hojas de cálculo. Esta combinación lo convierte en un escenario idóneo para aplicar los conceptos vistos en clase, ya que presenta los tres tipos de problemas que suelen encontrarse en la práctica profesional:

\begin{itemize}[leftmargin=*]
    \item \textbf{Problemas de diseño arquitectónico}: puntos únicos de falla, limitaciones de escalado, observabilidad parcial.
    \item \textbf{Problemas de ciberseguridad}: amenazas de spoofing, tampering, denegación de servicio e información expuesta.
    \item \textbf{Problemas de cumplimiento normativo}: ausencia de políticas de privacidad, falta de cifrado y de control de acceso basado en roles.
\end{itemize}

\subsection{Estructura del Documento}

El informe se organiza en tres partes principales, cada una correspondiente a uno de los talleres desarrollados, seguidas de una sección de integración de hallazgos y conclusiones generales:

\begin{enumerate}[leftmargin=*]
    \item \textbf{Parte I --- Taller 4}: Diagnóstico técnico de la infraestructura.
    \item \textbf{Parte II --- Taller 5}: Análisis de amenazas con el modelo STRIDE.
    \item \textbf{Parte III --- Taller 6}: Evaluación de cumplimiento normativo y gobierno de datos.
    \item \textbf{Parte IV}: Integración de hallazgos, conclusiones y referencias consolidadas.
\end{enumerate}

\newpage

% =============== PARTE I: TALLER 4 ===============
\section{Parte I --- Taller 4: Diagnóstico Técnico de Infraestructura}

\subsection{Descripción General del Sistema}

El sistema analizado es una \textbf{plataforma de gestión de propiedades y reservas} desplegada completamente en \textbf{AWS Cloud}. La arquitectura sigue un modelo orientado a microservicios con separación clara de capas: frontend, seguridad, API, cómputo, microservicios y datos. También integra plataformas externas como la \textbf{API de Airbnb} para sincronización de listados y reservas mediante webhooks.

Los usuarios principales del sistema son: inquilinos (\textit{Tenants}), administradores de propiedades (\textit{Property Managers}), personal de mantenimiento (\textit{Maintenance Staff}) y huéspedes de reserva (\textit{Booking Guests}).

\subsection{Mapa de Infraestructura por Capas}

\subsubsection{Capa de Frontend}
\begin{itemize}[leftmargin=*]
    \item \textbf{CDN} (\textit{Content Delivery Network}): distribuye contenido estático con baja latencia a nivel geográfico.
    \item \textbf{Web App (React)}: interfaz de usuario servida desde el CDN.
\end{itemize}

\subsubsection{Capa de Seguridad}
\begin{itemize}[leftmargin=*]
    \item \textbf{WAF (Web Application Firewall)}: filtra tráfico malicioso antes de que llegue a los servicios internos.
    \item \textbf{Authentication}: gestiona la autenticación de usuarios (presumiblemente mediante JWT o OAuth).
\end{itemize}

\subsubsection{Capa de API}
\begin{itemize}[leftmargin=*]
    \item \textbf{Load Balancer}: distribuye las solicitudes entrantes entre los servidores de cómputo.
    \item \textbf{Public API \& Webhooks}: punto de entrada para integraciones externas, incluyendo eventos de Airbnb.
\end{itemize}

\subsubsection{Capa de Cómputo}
\begin{itemize}[leftmargin=*]
    \item \textbf{API Server 1 y API Server 2}: dos instancias de servidor para procesamiento paralelo de solicitudes, lo que permite escalabilidad horizontal básica.
\end{itemize}

\subsubsection{Capa de Microservicios}
\begin{itemize}[leftmargin=*]
    \item \textbf{Integration Service}: gestiona la comunicación con plataformas externas.
    \item \textbf{Booking Service}: maneja la lógica de reservas.
    \item \textbf{Property Service}: administra los datos y operaciones relacionadas con propiedades.
\end{itemize}

\subsubsection{Cola de Eventos}
\begin{itemize}[leftmargin=*]
    \item \textbf{Message Queue}: desacopla la comunicación entre microservicios, permitiendo procesamiento asíncrono y resiliencia ante picos de carga.
\end{itemize}

\subsubsection{Capa de Datos}
\begin{itemize}[leftmargin=*]
    \item \textbf{Redis Cache}: caché en memoria para reducir la carga sobre la base de datos y mejorar tiempos de respuesta.
    \item \textbf{PostgreSQL Primary}: base de datos relacional principal.
    \item \textbf{PostgreSQL Replica}: réplica de lectura para alta disponibilidad y distribución de carga.
    \item \textbf{S3 Storage}: almacenamiento de objetos para backups y archivos estáticos.
    \item \textbf{Monitoring}: componente de observabilidad conectado a la capa de datos.
\end{itemize}

\subsubsection{Plataformas Externas}
\begin{itemize}[leftmargin=*]
    \item \textbf{Airbnb API}: sincroniza listados y reservas con el sistema mediante webhooks y eventos periódicos.
\end{itemize}

\subsection{Diagnóstico de Debilidades y Cuellos de Botella}

\subsubsection{Cuellos de Botella Identificados}

\begin{table}[H]
\centering
\caption{Cuellos de botella identificados en la infraestructura}
\renewcommand{\arraystretch}{1.3}
\begin{tabularx}{\textwidth}{|>{\raggedright\arraybackslash}p{3.2cm}|>{\raggedright\arraybackslash}X|>{\centering\arraybackslash}p{2.5cm}|}
\hline
\rowcolor{azulprincipal!15}
\textbf{Componente} & \textbf{Problema Potencial} & \textbf{Nivel de Riesgo} \\
\hline
Load Balancer & Punto único de falla si no tiene redundancia & \textcolor{rojoriesgo}{\textbf{Alto}} \\
\hline
WAF / Authentication & Si están en serie sin redundancia, una caída bloquea todo el acceso & \textcolor{rojoriesgo}{\textbf{Alto}} \\
\hline
PostgreSQL Primary & Toda la escritura pasa por un solo nodo; bajo carga alta puede ser cuello de botella & \textcolor{naranjariesgo}{\textbf{Medio-Alto}} \\
\hline
API Server 1 y 2 & Solo 2 instancias; ante picos de tráfico puede ser insuficiente sin autoescalado & \textcolor{naranjariesgo}{\textbf{Medio}} \\
\hline
Message Queue & Si la cola no tiene redundancia, los mensajes pueden perderse & \textcolor{naranjariesgo}{\textbf{Medio}} \\
\hline
\end{tabularx}
\end{table}

\subsubsection{Puntos Únicos de Falla (SPOF)}

\begin{itemize}[leftmargin=*]
    \item \textbf{Load Balancer}: no se evidencia un balanceador secundario ni configuración multi-AZ (múltiples zonas de disponibilidad) explícita en el mapa. Si falla, todo el tráfico queda bloqueado.
    \item \textbf{WAF}: un único WAF sin failover significa que un incidente en este componente puede hacer inaccesible todo el sistema.
    \item \textbf{PostgreSQL Primary}: aunque existe una réplica, la promoción automática de la réplica a primaria no siempre es instantánea, lo que puede generar ventanas de inactividad.
\end{itemize}

\subsubsection{Limitaciones de Escalabilidad}

El \textit{Compute Layer} muestra únicamente dos servidores de API sin indicación de un mecanismo de autoescalado (como AWS Auto Scaling Groups). Ante campañas de alta demanda, estos dos nodos podrían saturarse. Los microservicios (Integration, Booking, Property) no muestran réplicas ni políticas de escalado independiente, lo que puede limitar el rendimiento de servicios muy demandados (por ejemplo, Booking Service durante temporada alta). Adicionalmente, la integración con Airbnb API depende de un único flujo de sincronización; si este falla, no se visualiza un mecanismo de reintento robusto o fallback.

\subsubsection{Observabilidad y Monitoreo}

El componente de \textit{Monitoring} aparece únicamente conectado a la capa de datos. No se evidencia monitoreo explícito del Compute Layer, los microservicios ni la capa de API, lo que reduce la visibilidad ante fallos en esas capas. Se recomienda extender la observabilidad a todos los componentes críticos (Load Balancer, API Servers, microservicios) con métricas de CPU, latencia, tasa de errores y disponibilidad.

\subsubsection{Seguridad}

El WAF es el primer filtro de seguridad, lo cual es una buena práctica. Sin embargo, no se visualizan controles de seguridad internos entre microservicios (comunicación inter-servicio sin autenticación mutua podría ser un riesgo). Tampoco se aprecia cifrado explícito en tránsito entre capas internas, aunque podría estar implícito en la configuración de AWS.

\subsection{Oportunidades de Mejora}

\subsubsection{Alta Disponibilidad}
\begin{itemize}[leftmargin=*]
    \item Desplegar el Load Balancer y el WAF en \textbf{múltiples zonas de disponibilidad (Multi-AZ)} para eliminar puntos únicos de falla.
    \item Configurar \textbf{failover automático} entre PostgreSQL Primary y Replica mediante herramientas como AWS RDS Multi-AZ o Patroni.
\end{itemize}

\subsubsection{Escalabilidad}
\begin{itemize}[leftmargin=*]
    \item Implementar \textbf{AWS Auto Scaling Groups} en el Compute Layer para escalar automáticamente el número de API Servers según la carga.
    \item Evaluar el escalado independiente de cada microservicio mediante \textbf{AWS ECS} o \textbf{Kubernetes (EKS)}, de manera que el Booking Service pueda escalar de forma autónoma durante picos de reservas.
\end{itemize}

\subsubsection{Observabilidad}
\begin{itemize}[leftmargin=*]
    \item Extender el monitoreo a todas las capas utilizando herramientas como \textbf{CloudWatch}, \textbf{Prometheus + Grafana} o \textbf{Datadog}.
    \item Implementar \textbf{alertas proactivas} para detectar degradación de rendimiento antes de que impacte a los usuarios.
\end{itemize}

\subsubsection{Resiliencia en Integración Externa}
\begin{itemize}[leftmargin=*]
    \item Implementar un \textbf{mecanismo de reintentos con backoff exponencial} para los webhooks de Airbnb.
    \item Considerar un patrón \textbf{Circuit Breaker} para aislar fallos en la integración externa.
\end{itemize}

\subsubsection{Seguridad Interna}
\begin{itemize}[leftmargin=*]
    \item Adoptar un modelo de \textbf{Zero Trust} entre microservicios, con autenticación mutua (mTLS) o tokens de servicio internos.
    \item Realizar \textbf{auditorías de acceso} periódicas sobre la capa de datos y los microservicios.
\end{itemize}

\subsection{Conclusión del Taller 4}

La arquitectura analizada representa un diseño moderno y bien estructurado sobre AWS Cloud, con separación de responsabilidades por capas, uso de microservicios, caché, cola de mensajes y replicación de base de datos. Estas características son señales positivas de una infraestructura pensada para escalar.

Sin embargo, el diagnóstico revela oportunidades importantes en tres frentes: \textbf{eliminar puntos únicos de falla} (Load Balancer, WAF, base de datos primaria), \textbf{extender los mecanismos de escalado automático} (Compute Layer y microservicios), y \textbf{ampliar la cobertura de observabilidad} más allá de la capa de datos. Abordar estas mejoras permitiría al sistema soportar de manera confiable escenarios de alta demanda y garantizar la continuidad del negocio ante fallos inesperados.

\newpage

% =============== PARTE II: TALLER 5 ===============
\section{Parte II --- Taller 5: Análisis de Amenazas con el Modelo STRIDE}

\subsection{Introducción al Taller 5}

El Taller 5 tuvo como objetivo aplicar el modelo \textbf{STRIDE} para identificar amenazas de ciberseguridad sobre los componentes críticos del sistema analizado en el Taller 4. El modelo STRIDE, desarrollado por Microsoft, clasifica las amenazas en seis categorías: \textit{Spoofing} (suplantación de identidad), \textit{Tampering} (manipulación), \textit{Repudiation} (repudio), \textit{Information Disclosure} (divulgación de información), \textit{Denial of Service} (denegación de servicio) y \textit{Elevation of Privilege} (elevación de privilegios).

Este análisis toma como insumo el mapa de infraestructura construido en el Taller 4 y lo enriquece con una perspectiva defensiva, identificando para cada componente crítico qué tipo de ataque podría sufrir, cuál sería su impacto y qué control mitigante se propone implementar.

\subsection{Tabla STRIDE --- Análisis de Amenazas por Componente}

\begin{table}[H]
\centering
\caption{Matriz STRIDE aplicada al sistema del cliente}
\small
\renewcommand{\arraystretch}{1.3}
\begin{tabularx}{\textwidth}{|>{\raggedright\arraybackslash}p{2.6cm}|>{\raggedright\arraybackslash}p{2.2cm}|>{\raggedright\arraybackslash}X|>{\centering\arraybackslash}p{1.5cm}|}
\hline
\rowcolor{azulprincipal!15}
\textbf{Componente} & \textbf{Categoría STRIDE} & \textbf{Amenaza / Impacto / Control propuesto} & \textbf{Riesgo} \\
\hline

Autenticación de usuarios & Spoofing &
\textbf{Amenaza:} Un atacante roba credenciales y se hace pasar por un administrador. \newline
\textbf{Impacto:} Acceso no autorizado a reservas y datos de clientes. \newline
\textbf{Control:} Autenticación multifactor (MFA), contraseñas seguras y monitoreo de login. &
\textcolor{rojoriesgo}{\textbf{Alto}} \\
\hline

API de reservas & Tampering &
\textbf{Amenaza:} Manipulación de solicitudes de reserva enviadas al servidor. \newline
\textbf{Impacto:} Reservas incorrectas o pérdidas financieras. \newline
\textbf{Control:} Validación de solicitudes, tokens de autenticación y HTTPS. &
\textcolor{rojoriesgo}{\textbf{Alto}} \\
\hline

Base de datos de reservas & Repudiation &
\textbf{Amenaza:} Un usuario niega haber realizado una reserva o modificación. \newline
\textbf{Impacto:} Disputas y falta de trazabilidad. \newline
\textbf{Control:} Registro de auditoría (logs) con timestamps y seguimiento de usuarios. &
\textcolor{naranjariesgo}{\textbf{Medio}} \\
\hline

Base de datos de clientes & Information Disclosure &
\textbf{Amenaza:} Exposición de datos personales de clientes. \newline
\textbf{Impacto:} Violación de privacidad y problemas legales. \newline
\textbf{Control:} Cifrado de datos y control de acceso basado en roles. &
\textcolor{rojoriesgo}{\textbf{Alto}} \\
\hline

Infraestructura de la plataforma & Denial of Service &
\textbf{Amenaza:} Ataque de tráfico masivo que sobrecarga el sistema. \newline
\textbf{Impacto:} Caída del sistema e imposibilidad de hacer reservas. \newline
\textbf{Control:} Rate limiting, balanceadores de carga y protección DDoS. &
\textcolor{rojoriesgo}{\textbf{Alto}} \\
\hline

Módulo de mantenimiento & Elevation of Privilege &
\textbf{Amenaza:} Personal de mantenimiento obtiene permisos de administrador. \newline
\textbf{Impacto:} Control indebido del sistema. \newline
\textbf{Control:} Control de permisos por roles y revisión de accesos. &
\textcolor{naranjariesgo}{\textbf{Medio}} \\
\hline

Integración con API externa & Tampering / Info. Disclosure &
\textbf{Amenaza:} Manipulación de datos entre el sistema y plataformas externas. \newline
\textbf{Impacto:} Reservas duplicadas o filtración de datos. \newline
\textbf{Control:} Validación de webhooks, claves API seguras y cifrado. &
\textcolor{naranjariesgo}{\textbf{Medio}} \\
\hline

\end{tabularx}
\end{table}

\subsection{Análisis de Resultados}

Del análisis STRIDE se desprenden varias observaciones relevantes. En primer lugar, las amenazas de mayor impacto (clasificadas como \textit{Alto}) se concentran en tres puntos: la \textbf{autenticación de usuarios}, la \textbf{API de reservas} y la \textbf{base de datos de clientes}. Estos tres componentes conforman el eje crítico del sistema, ya que son los que manejan directamente la identidad de los usuarios y los datos sensibles.

En segundo lugar, se identifica que la mayoría de los controles propuestos son técnicamente implementables con tecnologías estándar ampliamente disponibles (MFA, HTTPS, cifrado, logs, RBAC). Esto significa que el gap de seguridad no se debe a limitaciones tecnológicas sino a una falta de implementación formal de controles que ya son de uso común en la industria.

En tercer lugar, el análisis confirma un hallazgo del Taller 4: la exposición a \textbf{ataques de denegación de servicio (DoS)} sobre la infraestructura. Aunque el sistema cuenta con un WAF y un balanceador de carga, la ausencia de políticas explícitas de \textit{rate limiting} y protección DDoS deja una ventana de vulnerabilidad que debe cerrarse.

\subsection{Buenas Prácticas de Ciberseguridad Aplicables}

A partir de la investigación complementaria se identificaron los siguientes marcos de referencia aplicables al sistema:

\begin{itemize}[leftmargin=*]
    \item \textbf{OWASP Top 10}: identifica las vulnerabilidades más críticas en aplicaciones web, incluyendo problemas de autenticación, exposición de datos sensibles y control de accesos.
    \item \textbf{Seguridad en la nube}: las arquitecturas cloud modernas implementan cifrado, monitoreo y control de accesos para proteger datos y servicios.
    \item \textbf{NIST Cybersecurity Framework}: propone cinco funciones principales para proteger sistemas: identificar, proteger, detectar, responder y recuperar frente a incidentes.
    \item \textbf{Seguridad en APIs (OWASP API Security)}: las APIs deben implementar autenticación fuerte, validación de solicitudes y limitación de tráfico para evitar accesos no autorizados o manipulación de datos.
    \item \textbf{Protección contra ataques DDoS}: utilización de balanceadores de carga y filtrado de tráfico para protegerse contra ataques de denegación de servicio.
\end{itemize}

\subsection{Conclusión del Taller 5}

El análisis STRIDE evidenció que el sistema presenta exposiciones relevantes en las seis categorías de amenaza, con tres de ellas clasificadas como de \textit{alto riesgo}. La implementación de los controles propuestos (MFA, cifrado, logs, RBAC, protección DDoS, validación de webhooks) debería tratarse como una prioridad a corto plazo, especialmente porque se trata de controles estándar cuya ausencia constituye una desviación notable respecto a las buenas prácticas de la industria y a marcos como OWASP y NIST.

\newpage

% =============== PARTE III: TALLER 6 ===============
\section{Parte III --- Taller 6: Evaluación de Cumplimiento Normativo}

\subsection{Introducción al Taller 6}

El presente componente tiene como objetivo evaluar el nivel de cumplimiento normativo del sistema de gestión de propiedades y reservas utilizado por el cliente. Este sistema administra información relacionada con clientes, reservas, inventario y operaciones, e incluye integraciones con plataformas externas como Airbnb. Dado que el sistema maneja datos personales, es necesario analizar su alineación con normativas nacionales e internacionales de protección de datos y seguridad de la información.

\subsection{Marco Normativo Aplicable}

El análisis se realizó teniendo en cuenta los siguientes marcos normativos:

\begin{itemize}[leftmargin=*]
    \item \textbf{Ley 1581 de 2012 (Colombia)}: regula la protección de datos personales y establece principios como legalidad, finalidad, libertad, veracidad, transparencia y seguridad.
    \item \textbf{Habeas Data}: garantiza el derecho de los usuarios a conocer, actualizar y rectificar su información personal.
    \item \textbf{ISO/IEC 27001}: estándar internacional para la gestión de la seguridad de la información, enfocado en la confidencialidad, integridad y disponibilidad.
    \item \textbf{Lineamientos MinTIC}: buenas prácticas promovidas por el Ministerio de Tecnologías de la Información y las Comunicaciones.
\end{itemize}

\subsection{Descripción del Sistema Evaluado}

El sistema analizado corresponde a una plataforma digital que permite gestionar propiedades en alquiler, administrar reservas y disponibilidad, manejar inventarios asociados a cada propiedad, registrar información de clientes e integrarse con plataformas externas como Airbnb para sincronización de reservas. Actualmente, gran parte de la operación se apoya en herramientas como Excel, lo cual incrementa el riesgo de pérdida de información y falta de control.

\subsection{Checklist de Cumplimiento (Gobierno de Datos)}

\begin{table}[H]
\centering
\caption{Checklist general de cumplimiento normativo}
\small
\renewcommand{\arraystretch}{1.3}
\begin{tabularx}{\textwidth}{|c|>{\raggedright\arraybackslash}p{2.3cm}|>{\raggedright\arraybackslash}X|>{\centering\arraybackslash}p{1.3cm}|>{\raggedright\arraybackslash}p{3.2cm}|}
\hline
\rowcolor{azulprincipal!15}
\textbf{N°} & \textbf{Categoría} & \textbf{Criterio} & \textbf{Nivel} & \textbf{Evidencia / Recomendación} \\
\hline
1 & Consentimiento & Se solicita autorización para el tratamiento de datos personales & \textcolor{naranjariesgo}{\textbf{Parcial}} & Implementar checkbox de consentimiento y política de privacidad \\
\hline
2 & Datos personales & Se recolectan solo los datos necesarios & \textcolor{naranjariesgo}{\textbf{Parcial}} & Aplicar principio de minimización de datos \\
\hline
3 & Seguridad & La información está protegida mediante cifrado & \textcolor{rojoriesgo}{\textbf{No cumple}} & Implementar HTTPS y cifrado en base de datos \\
\hline
4 & Acceso & Existe control de acceso por roles & \textcolor{naranjariesgo}{\textbf{Parcial}} & Implementar RBAC con roles claramente definidos \\
\hline
5 & Auditoría & Se registran logs de actividad del sistema & \textcolor{rojoriesgo}{\textbf{No cumple}} & Implementar sistema de logs y monitoreo \\
\hline
6 & Retención & Se define política de retención de datos & \textcolor{rojoriesgo}{\textbf{No cumple}} & Definir política de retención y eliminación \\
\hline
7 & Integraciones & Las APIs externas son seguras & \textcolor{naranjariesgo}{\textbf{Parcial}} & Usar autenticación segura, validación de webhooks y manejo seguro de API keys \\
\hline
8 & Disponibilidad & El sistema tiene mecanismos de alta disponibilidad & \textcolor{naranjariesgo}{\textbf{Parcial}} & Implementar backups, balanceadores y redundancia \\
\hline
9 & Derechos del usuario & El usuario puede acceder, modificar o eliminar sus datos & \textcolor{rojoriesgo}{\textbf{No cumple}} & Implementar módulo de gestión de datos del usuario \\
\hline
10 & Cumplimiento legal & Se cumple con la Ley 1581 de protección de datos & \textcolor{naranjariesgo}{\textbf{Parcial}} & Definir e implementar políticas formales de protección de datos \\
\hline
\end{tabularx}
\end{table}

\subsection{Resultados del Análisis de Cumplimiento}

\subsubsection{Cumplimientos Parciales}
Se evidencian algunos avances iniciales en:
\begin{itemize}[leftmargin=*]
    \item Gestión básica de información de clientes y reservas.
    \item Diferenciación de tipos de usuarios (administrador, personal operativo).
    \item Intención de implementar una arquitectura tecnológica más robusta.
\end{itemize}
Sin embargo, estos aspectos no están completamente formalizados ni alineados con estándares normativos.

\subsubsection{Brechas Identificadas}
Se detectaron múltiples brechas relevantes en materia de cumplimiento:
\begin{itemize}[leftmargin=*]
    \item Falta de consentimiento informado para el tratamiento de datos personales.
    \item Ausencia de políticas de privacidad y tratamiento de datos.
    \item No implementación de cifrado en almacenamiento o transmisión de información.
    \item Falta de control de acceso basado en roles (RBAC).
    \item Ausencia de registros de auditoría (logs).
    \item No definición de políticas de retención de datos.
    \item Limitaciones en la gestión de derechos del usuario (Habeas Data).
\end{itemize}
Estas brechas representan riesgos significativos en términos de seguridad, cumplimiento legal y confianza del usuario.

\subsection{Nivel de Madurez}

El sistema presenta un \textbf{nivel de madurez bajo} en cumplimiento normativo, ya que la mayoría de los controles requeridos por la Ley 1581 y estándares como ISO 27001 no están implementados o se encuentran en estado inicial.

\subsection{Riesgos Asociados}

Las debilidades identificadas pueden generar los siguientes riesgos:
\begin{itemize}[leftmargin=*]
    \item Exposición de datos personales de clientes.
    \item Sanciones legales por incumplimiento normativo.
    \item Pérdida de confianza por parte de usuarios y clientes.
    \item Inconsistencias en la información de reservas.
    \item Vulnerabilidad ante ataques o accesos no autorizados.
\end{itemize}

\subsection{Recomendaciones}

\subsubsection{Protección de Datos Personales}
\begin{itemize}[leftmargin=*]
    \item Implementar mecanismos de consentimiento informado.
    \item Definir y publicar una política de tratamiento de datos personales.
    \item Permitir a los usuarios ejercer sus derechos de acceso, modificación y eliminación de datos.
\end{itemize}

\subsubsection{Seguridad de la Información}
\begin{itemize}[leftmargin=*]
    \item Implementar cifrado de datos en tránsito (HTTPS) y en almacenamiento.
    \item Establecer controles de acceso basados en roles (RBAC).
    \item Implementar logs y monitoreo de actividades.
\end{itemize}

\subsubsection{Gestión Operativa}
\begin{itemize}[leftmargin=*]
    \item Definir una política de retención y eliminación de datos.
    \item Implementar backups automáticos y mecanismos de recuperación.
    \item Reducir la dependencia de herramientas manuales como Excel.
\end{itemize}

\subsubsection{Integraciones Externas}
\begin{itemize}[leftmargin=*]
    \item Asegurar la integración con Airbnb mediante validación de webhooks, uso de claves API seguras y control de accesos.
\end{itemize}

\subsection{Conclusión del Taller 6}

El análisis realizado evidencia que el sistema actual presenta importantes oportunidades de mejora en materia de cumplimiento normativo y seguridad de la información. Si bien la solución aún se encuentra en una etapa inicial de madurez, la adopción de una arquitectura moderna y la implementación de controles alineados con la Ley 1581 de 2012 y la norma ISO 27001 permitirán fortalecer la protección de datos, mejorar la confiabilidad del sistema y garantizar su escalabilidad futura.

\newpage

% =============== PARTE IV: INTEGRACIÓN Y CONCLUSIONES ===============
\section{Parte IV --- Integración de Hallazgos y Conclusiones Generales}

\subsection{Visión Integrada de los Tres Talleres}

La lectura conjunta de los tres talleres permite identificar un patrón claro: las debilidades detectadas en los tres frentes (arquitectura, seguridad y cumplimiento) \textbf{no son problemas aislados, sino manifestaciones distintas de las mismas causas raíz}. La siguiente tabla sintetiza cómo cada hallazgo técnico del Taller 4 se traduce en una amenaza concreta (Taller 5) y en una brecha de cumplimiento (Taller 6).

\begin{table}[H]
\centering
\caption{Integración de hallazgos entre los tres talleres}
\small
\renewcommand{\arraystretch}{1.4}
\begin{tabularx}{\textwidth}{|>{\raggedright\arraybackslash}p{3cm}|>{\raggedright\arraybackslash}X|>{\raggedright\arraybackslash}X|>{\raggedright\arraybackslash}X|}
\hline
\rowcolor{azulprincipal!15}
\textbf{Tema} & \textbf{T4 (Infraestructura)} & \textbf{T5 (STRIDE)} & \textbf{T6 (Cumplimiento)} \\
\hline
Autenticación y acceso & Authentication sin redundancia clara & Spoofing / Elevation of Privilege & Ausencia de RBAC formal \\
\hline
Datos de clientes & PostgreSQL sin cifrado explícito & Information Disclosure (Alto) & Criterio 3 y 9 no cumplidos \\
\hline
Trazabilidad & Monitoring solo en capa de datos & Repudiation sin logs & Criterio 5 (auditoría) no cumplido \\
\hline
Disponibilidad & SPOF en LB y WAF & Denial of Service (Alto) & Criterio 8 parcial \\
\hline
Integración Airbnb & Sin mecanismo de reintento robusto & Tampering / Info. Disclosure & Criterio 7 parcial \\
\hline
\end{tabularx}
\end{table}

\subsection{Plan de Acción Priorizado}

A partir de la integración de los tres análisis, se propone el siguiente orden de prioridad para las acciones correctivas, considerando tanto el impacto como la facilidad relativa de implementación:

\begin{enumerate}[leftmargin=*]
    \item \textbf{Corto plazo (crítico)}: Implementar HTTPS, cifrado de datos sensibles, MFA para cuentas administrativas y sistema de logs con timestamps. Estos controles atacan simultáneamente los tres frentes analizados.
    \item \textbf{Corto plazo (alto)}: Definir y publicar política de tratamiento de datos personales, implementar consentimiento informado y mecanismos de ejercicio de derechos del usuario. Cierra las brechas más visibles frente a la Ley 1581.
    \item \textbf{Mediano plazo}: Implementar RBAC formal, extender el monitoreo a todas las capas, configurar Multi-AZ para Load Balancer y WAF, y establecer mecanismos de reintento con \textit{backoff} para webhooks de Airbnb.
    \item \textbf{Mediano-largo plazo}: Migrar el Compute Layer a AWS Auto Scaling Groups o EKS, adoptar mTLS entre microservicios (Zero Trust) y reducir progresivamente la dependencia operativa de herramientas manuales (Excel).
\end{enumerate}

\subsection{Reflexión del Equipo sobre el Trabajo del Semestre}

El desarrollo de los tres talleres permitió al equipo \textbf{Cyber Nexus --- Grupo 7} recorrer de manera práctica el ciclo completo de evaluación de un sistema empresarial: desde la comprensión de su arquitectura hasta la verificación de su cumplimiento normativo, pasando por el análisis estructurado de amenazas. Este recorrido dejó varios aprendizajes clave para el equipo:

\begin{itemize}[leftmargin=*]
    \item \textbf{La arquitectura no es un tema puramente técnico}: toda decisión de diseño tiene implicaciones de seguridad y de cumplimiento que solo se hacen visibles cuando se miran las tres dimensiones simultáneamente.
    \item \textbf{Los marcos de referencia (STRIDE, OWASP, NIST, ISO 27001, Ley 1581) no son listas burocráticas}: son herramientas prácticas que ayudan a estructurar el análisis y a no dejar fuera aspectos críticos.
    \item \textbf{La mayoría de las mejoras recomendadas son implementables con tecnologías estándar}: el principal obstáculo no es técnico sino organizacional (falta de políticas formales, ausencia de procesos documentados, dependencia de herramientas manuales).
    \item \textbf{El trabajo en equipo con división de responsabilidades} fue determinante para cubrir los tres ejes con el nivel de detalle requerido en cada entrega.
\end{itemize}

\subsection{Conclusión General}

El trabajo realizado a lo largo del semestre sobre la plataforma de gestión de propiedades y reservas ha demostrado que, aunque el sistema cuenta con una base arquitectónica moderna desplegada en AWS, presenta \textbf{brechas significativas en las tres dimensiones analizadas}: alta disponibilidad y observabilidad en la infraestructura, controles técnicos de ciberseguridad y cumplimiento normativo frente a la Ley 1581 e ISO 27001.

Estas brechas no son triviales, pero tampoco son insalvables: la gran mayoría se cierra con controles estándar (MFA, HTTPS, cifrado, RBAC, logs, Multi-AZ) que, aplicados de forma coordinada, permitirían al sistema pasar de un nivel de madurez bajo a un nivel aceptable para operar en producción con datos personales de clientes.

Para el equipo, este proyecto integrador ha sido una oportunidad valiosa para aplicar de forma articulada los conceptos de arquitectura empresarial, ciberseguridad y gobierno de datos sobre un mismo caso de estudio. Consideramos que el ejercicio cumple con los objetivos del curso y, más allá de la calificación, nos deja un marco de análisis replicable para futuros proyectos profesionales.

\newpage

% =============== REFERENCIAS ===============
\section{Referencias Consolidadas}

\subsection{Arquitectura de Infraestructura (Taller 4)}
\begin{itemize}[leftmargin=*]
    \item Amazon Web Services. (2023). \textit{AWS Well-Architected Framework}. \url{https://aws.amazon.com/architecture/well-architected/}
    \item Microsoft Azure. (2023). \textit{Cloud Architecture Best Practices}. \url{https://learn.microsoft.com/en-us/azure/architecture/}
    \item Google Cloud. (2023). \textit{Infrastructure Architecture Framework}. \url{https://cloud.google.com/architecture}
\end{itemize}

\subsection{Ciberseguridad (Taller 5)}
\begin{itemize}[leftmargin=*]
    \item OWASP Foundation. \textit{OWASP Top Ten}. \url{https://owasp.org/www-project-top-ten/}
    \item OWASP Foundation. \textit{OWASP API Security Project}. \url{https://owasp.org/www-project-api-security/}
    \item NIST. \textit{Cybersecurity Framework}. \url{https://www.nist.gov/cyberframework}
    \item Amazon Web Services. \textit{AWS Cloud Security}. \url{https://aws.amazon.com/security/}
    \item Cloudflare. \textit{What is a DDoS Attack?} \url{https://www.cloudflare.com/learning/ddos/what-is-a-ddos-attack/}
\end{itemize}

\subsection{Cumplimiento Normativo (Taller 6)}
\begin{itemize}[leftmargin=*]
    \item Congreso de Colombia. (2012). \textit{Ley 1581 de 2012 --- Protección de Datos Personales}.
    \item ISO/IEC 27001. \textit{Information Security Management Systems}.
    \item Ministerio de Tecnologías de la Información y las Comunicaciones (MinTIC). \textit{Lineamientos de buenas prácticas en transformación digital y seguridad}.
    \item Habeas Data (Colombia) --- Derecho constitucional al acceso, rectificación y eliminación de información personal.
\end{itemize}

\vspace{1cm}

\begin{center}
\rule{0.5\linewidth}{0.4pt}\\[0.3cm]
\textit{Fin del informe consolidado}\\
\textbf{Cyber Nexus --- Grupo 7}\\
Arquitectura Empresarial --- Universidad de La Sabana
\end{center}

\end{document}
