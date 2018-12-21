FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 50161
EXPOSE 44398

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["BudgetCategoryService/BudgetCategoryService.csproj", "BudgetCategoryService/"]
RUN dotnet restore "BudgetCategoryService/BudgetCategoryService.csproj"
COPY . .
WORKDIR "/src/BudgetCategoryService"
RUN dotnet build "BudgetCategoryService.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "BudgetCategoryService.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "BudgetCategoryService.dll"]