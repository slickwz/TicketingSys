FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["TicketingSys.Interface/TicketingSys.Interface.csproj", "TicketingSys.Interface/"]
RUN dotnet restore "TicketingSys.Interface/TicketingSys.Interface.csproj"
COPY . .
WORKDIR "/src/TicketingSys.Interface"
RUN dotnet build "TicketingSys.Interface.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TicketingSys.Interface.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TicketingSys.Interface.dll"]