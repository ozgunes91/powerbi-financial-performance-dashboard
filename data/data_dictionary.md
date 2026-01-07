# Data Dictionary (high level)

This project uses a star-schema style model with a fact table and several dimensions.

## Fact table
- **FactSales**: transactional sales metrics (e.g., Sales, Profit, Units Sold) at a date/country/product/segment/discount granularity.

## Dimensions
- **DimDate**: calendar table (date attributes like year/month/day, YearMonth).
- **DimCountry**: country attributes (e.g., Country).
- **DimProduct**: product attributes (e.g., Product).
- **DimSegment**: customer segment attributes (e.g., Segment).
- **DimDiscountBand**: discount band attributes (e.g., DiscountBand).

> Note: Exact column names/types are defined in the PBIX model.
