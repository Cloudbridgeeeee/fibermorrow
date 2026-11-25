# FiberMorrow — proposed AWS architecture

FiberMorrow uses AWS to read purchasing documents, learn from your production history and forecast requirements — securely and per facility.

## Request flow

1. POs & delivery notes
2. Amazon S3
3. Textract
4. AWS Lambda
5. DynamoDB
6. SageMaker AI
7. Buyer approval

## Services

### Amazon SageMaker AI

**Role:** Forecast demand and lead times

Trains models on production orders, consumption and delivery history to forecast material requirements and supplier lead times with confidence ranges.

### Amazon Textract

**Role:** Read purchase orders and delivery notes

Extracts line items, quantities, prices and dates from POs, invoices and delivery notes — including scanned paper documents from suppliers.

### Amazon S3

**Role:** Store purchasing documents

Keeps original documents and exports encrypted and versioned, so every forecast can be traced back to its source data.

### Amazon DynamoDB

**Role:** Hold materials, orders and plans

Stores normalised materials, purchase orders, deliveries, forecasts and buyer decisions for fast access in the purchasing workspace.

### AWS Lambda

**Role:** Process documents and refresh forecasts

Runs the import pipeline, links deliveries to orders and refreshes forecasts and recommendations whenever new data arrives.

## Principles

- **Buyers decide** — Recommendations are proposals, never automatic orders.
- **Traceable numbers** — Every forecast links to the orders and deliveries behind it.
- **Supplier data private** — Prices and supplier terms are visible only to your team.

## Safeguards

- **No automatic orders** — FiberMorrow recommends; buyers approve every purchase.
- **Explained quantities** — Each recommendation shows demand, stock, buffer and lead time behind the number.
- **Extraction reviewed** — Low-confidence document fields are flagged for a person to check.
- **Commercial confidentiality** — Prices and supplier terms are encrypted and access-controlled.

## MVP scope

We import a year of purchase orders, deliveries and production orders for one facility, then deliver weekly material demand forecasts and purchase recommendations your buyers review.

- PO and delivery note import
- Material demand forecasts
- Supplier lead-time scores
- Purchase recommendations
- Weekly cost report
