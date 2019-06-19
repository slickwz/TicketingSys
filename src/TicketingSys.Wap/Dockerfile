FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["TicketingSys.Wap/TicketingSys.Wap.csproj", "TicketingSys.Wap/"]
RUN dotnet restore "TicketingSys.Wap/TicketingSys.Wap.csproj"
COPY . .
WORKDIR "/src/TicketingSys.Wap"
RUN dotnet build "TicketingSys.Wap.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TicketingSys.Wap.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TicketingSys.Wap.dll"]