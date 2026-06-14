# DHL Express GraphQL Schema

## Overview

This document describes a conceptual GraphQL schema for the DHL Express global shipping API. DHL Express provides express delivery services across more than 220 countries and territories. The DHL Unified API (REST) is documented at https://developer.dhl.com/ and covers shipment creation, tracking, rate quoting, pickup scheduling, label generation, and customs/clearance workflows.

This GraphQL schema models the core domain types drawn from the DHL Express REST API surface and represents how those capabilities could be expressed as a typed GraphQL interface.

## Source

- Developer portal: https://developer.dhl.com/
- API reference: https://developer.dhl.com/api-catalog
- GitHub: https://github.com/dhl-express

## Schema File

See `dhl-schema.graphql` for the full type definitions.

## Key Query Areas

### Shipment Tracking

Query shipment tracking events by waybill number or tracking number. Returns a `ShipmentTracking` object containing a list of `TrackingEvent` entries, each with a `Timestamp`, `Location`, and event description.

### Rate Quoting

Submit a `RateRequest` with shipper/recipient addresses, package dimensions and weight, and desired product codes to receive a list of `Rate` objects including base charges, `Surcharge` items, and delivery commitments.

### Shipment Creation

Create a shipment by submitting a `ShipmentRequest` with `ShipperInfo`, `RecipientInfo`, `Package` details, `Content`, `Product`, and optional `SpecialService` entries. The response is a `ShipmentResponse` containing the `TrackingNumber`, `Label`, and `WaybillDocument`.

### Pickup Scheduling

Submit a `PickupRequest` with `PickupAddress`, `PickupTime`, and piece count to receive a `PickupConfirmation`.

### Customs and Clearance

Attach `CommercialInvoice`, `Commodity` lines, `HarmonizCode`, `ExportInfo`, `ImportInfo`, and `Duties` to cross-border shipments.

## Type Summary

The schema defines 67 named types covering:

- Core shipment lifecycle: `Shipment`, `ShipmentRequest`, `ShipmentResponse`
- Tracking: `ShipmentTracking`, `TrackingEvent`, `TrackingNumber`, `Timestamp`
- Geography: `Location`, `Address`, `ServiceArea`, `ServiceAreaCode`
- Parties: `CustomerDetails`, `ShipperInfo`, `RecipientInfo`, `ShipperContact`, `RecipientContact`, `AccountDetails`, `Account`
- Packaging: `Package`, `Piece`, `PieceDetails`, `Weight`, `Dimension`, `PackagingType`
- Products and services: `Product`, `ProductName`, `ProductCode`, `Service`, `ServiceType`, `SpecialService`
- Rates: `RateRequest`, `RateResponse`, `Rate`, `Surcharge`
- Pickup: `PickupRequest`, `PickupDetails`, `PickupConfirmation`, `PickupAddress`, `PickupTime`
- Labels and documents: `Label`, `LabelFormat`, `WaybillDocument`
- Customs: `CommercialInvoice`, `ClearanceData`, `Commodity`, `HarmonizCode`, `ExportInfo`, `ImportInfo`, `Content`
- Financials: `Duties`, `DutiesPayment`, `Insurance`, `InsuredAmount`
- Dangerous goods: `DangerousGoods`
- Notifications: `NotificationRequest`, `Webhook`
- Auth: `APIKey`, `Token`
