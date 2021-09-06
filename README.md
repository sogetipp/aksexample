# Introducción

Este repositorio contiene los recursos necesarios para la formación de AKS impartido en Sogeti a finales del año 2021. Con estos recursos más el contenido de la formación en sí, son suficientes para hacer lo siguiente:

1. desarrollar dos microservicios con arquitectura DDD en C# y .Net 5, 
2. a partir de ellos crear los contenedores Docker, 
3. publicarlos en ACR (creando un ACR si es necesario),
4. configurar el despliegue a partir de un archivo YAML y
5. desplegar el cluster en AKS.

Los microservicios de ejemplo se comunicarán y uno de ellos le servirá una colección de DTOs al otro. Los tipos DTO se obtendrán de nuget.org/packages/Sogeti.Literature.Dtos/.

# Contenido del repositorio

## aks-deployment.yaml

Archivo de configuración en YAML que describe el cluster Kubernetes del ejemplo.

## Sogeti.Template.DddMicroservice.vsix

Plantilla para crear automáticamente la solución y los proyectos de los microservicios de ejemplo. Es un archivo ejecutable VSIX que instala la plantilla en Visual Studio. Tras la instalación, solo hay que crear un nuevo proyecto y buscar la plantilla por Sogeti.

## how to deploy AKS in commands.txt

Archivo de ayuda con todos los comandos (y alguno más) correspondientes a la formación de AKS. Estos comandos son el día a día de un desarrollador de microservicios desplegados en AKS.

# Troubleshooting

Al crear un microservicio a partir de la plantilla, la solución es directamente compilable y ejecutable. Sin embargo, es posible que ocurra el siguiente error de certificado HTTPS:

```
System.InvalidOperationException: 'Unable to configure HTTPS endpoint. No server certificate was specified, and the default developer certificate could not be found or is out of date.
To generate a developer certificate run 'dotnet dev-certs https'. To trust the certificate (Windows and macOS only) run 'dotnet dev-certs https --trust'.
For more information on configuring HTTPS see https://go.microsoft.com/fwlink/?linkid=848054.'
```

Se recomienda visitar la web indicada en el error, https://go.microsoft.com/fwlink/?linkid=848054. El problema es que el certificado incluido como parte del SDK .Net Core no está verificado (_trusted_). Para verificarlo, hay que abrir una consola y ejecutar el siguiente comando:

```
dotnet dev-certs https --trust
```

Después de esto y de reiniciar Visual Studio, el error debería haber desaparecido.