# Billing API

FastAPI invoice and payment-state service for SparrowX. It manages invoices, stores state in the Crossplane-managed `billingdb` PostgreSQL database, and exposes health and Prometheus metrics endpoints.

The API is under `/api/billing/`, with invoice retrieval and pay/cancel actions under `/api/billing/{invoice_id}`. `/health` serves probes, `/api/billing/health` is the smoke test, `/metrics` exposes metrics, and `/docs`/`/redoc` provide API documentation.

Argo CD deploys `helm-values-dev.yaml` and `helm-values-prod.yaml` into separate `dev` and `prod` namespaces on one EKS cluster. Shared workflows build immutable images, run tests and security gates, promote by digest, and validate the resulting deployment.

Define `HEALTH_CHECK_PATH`; define `AWS_ROLE_NAME` only to override the organization’s default OIDC role. AWS account/region, environment URLs, and Argo CD credentials are shared.

## Local development

```bash
python -m pip install -r requirements-dev.txt
pytest
uvicorn src.main:app --reload --port 8000
```

Configure `DB_HOST`, `DB_PORT`, `DB_NAME`, `DB_USERNAME`, `DB_PASSWORD`, and optional `CORS_ALLOW_ORIGINS`.

## License

See [LICENSE.md](LICENSE.md).
