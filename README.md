# Fintech.E2E

End-to-end test harness for the Fintech microservices ecosystem. Validates cross-service flows by running real services via Docker Compose.

## Status

**Skeleton** — project structure exists but no real test scenarios are implemented yet.

## Architecture

```
Fintech.E2E/
├── Fintech.E2E.sln
├── Fintech.E2E/
│   └── Fintech.E2E.csproj        # xUnit test project
└── docker-compose.yml             # Infrastructure (RabbitMQ only, currently)
```

## Technology stack

| Component | Version |
|---|---|
| .NET | 8.0 |
| xUnit | latest |
| Docker Compose | RabbitMQ 3.x |

## Commands

```bash
# Build
dotnet build Fintech.E2E.sln

# Run tests (requires Docker services)
docker compose up -d
dotnet test Fintech.E2E.sln
```

## Planned test scenarios

- Accounts -> Notifications flow: transfer funds, verify notification persisted (FIN-43)
- Tasker -> OpsFlow flow: submit task, verify operational task created
- OpsFlow -> Notifications flow: transition task, verify notification triggered

## Services under test

| Service | Role |
|---|---|
| Fintech.Accounts | Produces TransferCompleted events |
| Fintech.Notifications | Consumes and persists transfer events |
| Tasker | Produces OperationalTaskSubmitted events |
| OpsFlow | Consumes operational tasks, produces state change events |
