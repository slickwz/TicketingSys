FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["TicketingSys.Web/TicketingSys.Web.csproj", "TicketingSys.Web/"]
RUN dotnet restore "TicketingSys.Web/TicketingSys.Web.csproj"
COPY . .
WORKDIR "/src/TicketingSys.Web"
RUN dotnet build "TicketingSys.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TicketingSys.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TicketingSys.Web.dll"]