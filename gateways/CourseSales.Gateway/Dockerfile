FROM mcr.microsoft.com/dotnet/sdk:8.0-bookworm-slim as sdk
WORKDIR /app
EXPOSE 80

COPY gateways/CourseSales.Gateway/CourseSales.Gateway.csproj gateways/CourseSales.Gateway/
#COPY gateways/CourseSales.Gateway/*.csproj gateways/CourseSales.Gateway/
#RUN dotnet restore gateways/CourseSales.Gateway/*.csproj
RUN dotnet restore gateways/CourseSales.Gateway/CourseSales.Gateway.csproj

# . . diyerek app içerisindekileri app içerisinde kopyala diyoruz. yukarıdaki kopyaladıklarım haricindeki herşeyi kopyala
COPY . . 
RUN dotnet publish gateways/CourseSales.Gateway/CourseSales.Gateway.csproj -c Release -o GatewayPublishFolder
#RUN dotnet publish gateways/CourseSales.Gateway/*.csproj -c Release -o GatewayPublishFolder
FROM mcr.microsoft.com/dotnet/aspnet:8.0 as runtime

WORKDIR /app
#sdk image'inden kopyala. sdk image içerisindeki /app/CatalogPublishFolder klasörünü, runtime içerisindeki app'in içine kopyala
COPY --from=sdk /app/GatewayPublishFolder .
ENTRYPOINT [ "dotnet", "CourseSales.Gateway.dll" ]