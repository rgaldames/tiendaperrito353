# Tienda Perritos

> **Proyecto Académico:** Despliegue Automatizado en Amazon EKS con GitHub Actions  
> **Asignatura:**  INTRODUCCION A HERRAMIENTAS DEVOPS_006V  

**Evaluaciónes: 1,2,3**  
---
## Dominio: 

1. Amazon EKS  
2. Amazon ECS  
3. Amazon ECR  
4. Amazon EC2  
5. Amazon VPC  
6. Internet Gateway  
7. NAT Gateway  
8. Security Groups  
9. Elastic Load Balancer (ELB / ALB)  
10. AWS IAM  
11. Amazon CloudWatch  
12. AWS CLI  
13. AWS Academy  
14. Amazon S3  
15. GitHub Actions  
16. GitHub Secrets y variables  


---
## Descripción:
Este repositorio documenta el proceso completo para orquestar y automatizar el despliegue de una aplicación ("Tienda de Perritos") utilizando contenedores y herramientas metodológicas de DevOps

A continuación, se detalla el resumen de las etapas realizadas:
---
Actividad 3.1: 
**Fundamentos de la orquestación de contenedores**
En esta etapa se abordan las bases teóricas que justifican el uso de plataformas como Kubernetes y Amazon EKS en lugar de contenedores aislados

Se analizan los componentes que hacen posible la alta disponibilidad a través del balanceo de carga, el autoescalado y la administración distribuida

Además, se establece la relación fundamental entre la orquestación y los ciclos de CI/CD dentro del enfoque DevOps
---
Actividad 3.2: 
**Implementación de infraestructura base en AWS**
Esta es la fase práctica más extensa, orientada a construir el entorno en la nube

Los hitos principales son:
Creación del Clúster EKS: Configuración del Control Plane gestionado por AWS y creación de los Node Groups (servidores worker) desplegados en subredes privadas

Conexión del entorno: Vinculación de la terminal local al clúster en la nube utilizando AWS CLI y la herramienta kubectl

Gestión de imágenes Docker: Autenticación, empaquetado (build) y publicación (push) de las imágenes del frontend, backend y base de datos en el repositorio de Amazon ECR

Despliegue manual: Aplicación de los archivos de configuración YAML para instruir a Kubernetes en la creación de los Deployments y Services

Exposición a internet: Configuración de un servicio tipo LoadBalancer para obtener una URL pública y acceder a la aplicación web desde el navegador
---
Actividad 3.3: 
**Integración teórica de CI/CD**
Funciona como el puente conceptual hacia la automatización

En esta etapa se validan los conocimientos sobre la integración y entrega continua (CI/CD), el rol de GitHub Actions en la ejecución de pipelines, y cómo se aplican actualizaciones automáticas (rolling updates) a través de manifiestos YAML en Kubernetes
---
Actividad 3.4: 
**Construcción del Pipeline automatizado**
Se implementa la automatización del despliegue directamente desde el repositorio
Incluye los siguientes pasos técnicos:
Control de versiones: Creación del repositorio en GitHub y subida de todas las capas del proyecto (frontend, backend, base de datos y carpeta de manifiestos k8s)

Seguridad: Configuración segura de las variables y Secrets en GitHub, inyectando las credenciales temporales de AWS Academy (AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_SESSION_TOKEN) para permitir la comunicación remota

Creación del Workflow: Diseño del archivo de automatización .github/workflows/deploy-eks.yml, el cual define las instrucciones exactas para construir las nuevas imágenes, subirlas a ECR y actualizar el clúster usando kubectl
---
Actividad 3.5: 
**Ejecución y validación del Pipeline CI/CD**
Corresponde a la prueba de fuego del flujo automatizado

Las validaciones incluyen:
Ejecución de GitHub Actions: Disparar el pipeline y monitorear que cada tarea (job) configurada en el workflow finalice exitosamente en color verde

Validación en el Clúster: Verificar mediante comandos kubectl get pods -n tienda y kubectl get svc -n tienda que las réplicas fueron actualizadas y se encuentran en estado óptimo

Prueba de acceso: Extraer la IP externa (EXTERNAL-IP) asignada al frontend y cargarla en el navegador para confirmar que la aplicación está pública, funcional y actualizada

A continuación se detalla la lista de herramientas, comandos y servicios de AWS, Git y GitHub mencionados a lo largo de la documentación y nuestra conversación:
---
**Herramientas y Servicios de AWS**
**Amazon EKS (Elastic Kubernetes Service):** 
El servicio principal utilizado para orquestar y administrar el clúster de Kubernetes en la nube

**Amazon ECS (Elastic Container Service):** Mencionado teóricamente como otro orquestador de contenedores nativo de AWS alternativo a EKS

**Amazon ECR (Elastic Container Registry):** El repositorio utilizado para empaquetar, almacenar y descargar las versiones de las imágenes Docker (frontend, backend, base de datos) de la aplicación

**Amazon EC2 (Elastic Compute Cloud):** Las máquinas virtuales que actúan como "worker nodes" (nodos de trabajo) agrupadas en un Node Group. Se configuran usando instancias tipo SPOT de tamaño t3.large

**Amazon VPC (Virtual Private Cloud):** El servicio base para crear la arquitectura de red

---

## Incluye componentes como:
Subredes (Públicas y Privadas): Para aislar o exponer los recursos

Internet Gateway (IGW) y Tablas de Ruteo: Para dar salida a internet a las subredes públicas

NAT Gateway: Servicio para dar salida a internet a subredes privadas, aunque en el laboratorio se omitió para ahorrar créditos

Security Groups: Para definir reglas de firewall, como permitir tráfico HTTP/HTTPS en el puerto 80/443

Elastic Load Balancer (ELB / ALB): El balanceador de carga aprovisionado automáticamente por Kubernetes para exponer públicamente el frontend hacia internet

AWS IAM (Identity and Access Management): Utilizado para gestionar permisos mediante la asignación de roles clave como LabEKSClusterRole y LabEKSNodeRole

Amazon CloudWatch: Herramienta de observabilidad utilizada para recolectar logs (registros) del plano de control de Kubernetes y monitorear métricas de consumo del clúster

AWS CLI (Command Line Interface): La herramienta de consola para interactuar con los recursos de AWS en tu entorno local

**Se utilizaron comandos como:**
aws configure y aws sts get-caller-identity para configurar y validar credenciales

aws eks update-kubeconfig para enlazar el clúster con la terminal local

aws ecr get-login-password para autenticar Docker con el repositorio de imágenes

**AWS Academy (Vocareum / Learner Lab):**
 La plataforma educativa que provee el entorno de nube y los tokens temporales (AWS_SESSION_TOKEN) para realizar la actividad

**Amazon S3:** Mencionado en el contexto de configurar puntos de enlace (VPC Endpoints/Gateways) para tráfico privado hacia buckets de almacenamiento

---

## Comandos de Git

Se utilizó Git como sistema de control de versiones local para subir el código del proyecto. Los comandos específicos empleados son:
git init: Para inicializar el repositorio local en la carpeta del proyecto

git status: Para comprobar el estado de los archivos modificados

git add: Para añadir archivos al área de preparación (ej. git add . para todo, o git add index.html para un archivo específico)

git commit: Para empaquetar los cambios con un mensaje descriptivo (ej. git commit -m "...")

git branch: Para renombrar y fijar la rama principal (ej. git branch -M main)

git remote: Para vincular el repositorio local con la URL del repositorio remoto (ej. git remote add origin)

git pull: Para descargar cambios desde el servidor remoto antes de subir nuevos cambios (ej. git pull --rebase origin main)

git push: Para enviar los commits empaquetados hacia la nube en GitHub

git reset: Para quitar un archivo del área de preparación si se añadió por error


## Herramientas y Características de GitHub
**GitHub Repositories:** El alojamiento remoto donde se almacenan todas las capas del proyecto (frontend, backend, bd y archivos k8s)

**GitHub Actions:** El motor que automatiza los pipelines de CI/CD (Integración y Entrega Continua) para construir imágenes, subirlas a ECR y actualizar el clúster automáticamente cuando hay un push

**GitHub Secrets y variables:** La funcionalidad de seguridad (en Settings > Secrets and variables > Actions) usada para almacenar las claves de acceso de AWS (AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_SESSION_TOKEN y AWS_REGION), permitiendo que el pipeline interactúe con AWS de forma segura y oculta


## RGS
-.-